---
layout: default
title: All 3D-OD Models
permalink: /models/
---

<section class="site-content">

# All 3D-Object-Detection Models

<p>Filter by sensor/representation, sort by year or mAP, and search any column.</p>

<div style="margin-bottom:1rem;">
  <button data-filter="" style="margin-right:.5rem;">All Models</button>
  <button data-filter="Monocular" style="margin-right:.5rem;">Monocular</button>
  <button data-filter="Stereo" style="margin-right:.5rem;">Stereo</button>
  <button data-filter="LiDAR" style="margin-right:.5rem;">LiDAR</button>
  <button data-filter="Multiview" style="margin-right:.5rem;">Multiview</button>
  <button data-filter="Multi-Modal">Multi-Modal</button>
</div>

<table id="models-table" class="display" style="width:100%">
  <thead>
    <tr id="models-header-row"></tr>
  </thead>
</table>

</section>

<script>
$(document).ready(function(){
  Papa.parse("{{ '/assets/data/models.csv' | relative_url }}", {
    download: true,
    header: true,
    dynamicTyping: true,
    skipEmptyLines: true,
    complete: function(results) {
      // 1) Remove that extra second-row-of-subheaders by filtering out any row
      //    where the Method field is blank or literally equals the header string.
      const data = results.data.filter(r => {
        const m = r.Method;
        return m != null && m.toString().trim() !== '' && m.toString().trim() !== 'Method';
      });

      // 2) Grab the real header names
      const fields = results.meta.fields;

      // 3) Populate <thead>
      const $hdr = $('#models-header-row');
      fields.forEach(f => $hdr.append(`<th>${f.trim()}</th>`));

      // 4) Build columns config
      const columns = fields.map((f, idx) => ({
        data: f,
        title: f.trim(),
        render: idx === fields.length - 1
          ? d => d ? `<a href="${d}" target="_blank">📄</a>` : ''
          : undefined
      }));

      // 5) Initialize DataTable
      const table = $('#models-table').DataTable({
        data,
        columns,
        pageLength: 25,
        order: [[ fields.indexOf('Year'), 'desc' ]],
        columnDefs: [
          // center the numeric AP columns (likely cols 5–13)
          { targets: Array.from({length:9}, (_, i) => i + 5), className: 'dt-center' }
        ]
      });

      // 6) Filter buttons for “Representation”
      const repIdx = fields.indexOf('Representation');
      $('button[data-filter]').on('click', function(){
        const val = $(this).data('filter');
        if (!val) {
          table.search('').column(repIdx).search('').draw();
        } else {
          table.search('').column(repIdx)
               .search(`^${val}$`, true, false)
               .draw();
        }
      });
    }
  });
});
</script>
