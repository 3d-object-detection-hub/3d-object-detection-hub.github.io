---
layout: default
title: 3D Object Detection
permalink: /3d-object-detection/
---


# 3D-Object-Detection Models

<p>Filter by sensor (primary), then by representation (secondary). Sort by sensor → representation → year (ascending) → month (ascending), and search any column.</p>

<!-- Primary sensor filters -->
<strong>Filter by sensor:</strong>
<div id="sensor-filters" style="margin:1rem 0;">
  <button data-sensor="All">All Models</button>
  <button data-sensor="Camera">Camera</button>
  <button data-sensor="LiDAR">LiDAR</button>
  <button data-sensor="Multi-Modal">Multi-Modal</button>
</div>

<!-- Secondary representation filters (hidden until a sensor is selected) -->
<div id="rep-filters" style="margin-bottom:1rem;">
  <div class="rep-group" data-sensor="Camera" style="display:none;">
    <button data-rep="Monocular">Monocular</button>
    <button data-rep="Stereo">Stereo</button>
    <button data-rep="Multiview">Multiview</button>
  </div>
  <div class="rep-group" data-sensor="LiDAR" style="display:none;">
    <button data-rep="Projection">Projection</button>
    <button data-rep="Point">Point</button>
    <button data-rep="Voxel">Voxel</button>
    <button data-rep="Point-Voxel">Point-Voxel</button>
  </div>
  <div class="rep-group" data-sensor="Multi-Modal" style="display:none;">
    <button data-rep="Early-Fusion">Early-Fusion</button>
    <button data-rep="Mid-Fusion">Mid-Fusion</button>
    <button data-rep="Intermediate">Intermediate</button>
    <button data-rep="Late-Fusion">Late-Fusion</button>
  </div>
</div>

<table id="models-table" class="display" style="width:100%">
  <thead>
    <tr id="models-header-row"></tr>
  </thead>
</table>

<!-- Parameter descriptions -->
<div class="table-description" style="margin-top:1.5em; font-size:0.9em; line-height:1.4;">
  <strong>Parameter descriptions:</strong>
  <ul>
    <li><strong>AP2D / AP3D / APBEV:</strong> Easy (E), Moderate (M), Hard (H) on KITTI Car test</li>
    <li><strong>NuScenes mAP:</strong> Mean AP on nuScenes validation</li>
    <li><strong>NDS:</strong> nuScenes Detection Score</li>
    <li><strong>Waymo L1 / L2 mAP:</strong> Level-1 / Level-2 mAP on Waymo</li>
    <li><strong>Time (s):</strong> Inference time per frame (seconds)</li>
  </ul>
</div>

<section class="site-content">

</section>

<script>
$(document).ready(function(){
  const csvUrl = "{{ '/assets/data/models.csv' | relative_url }}";

  fetch(csvUrl)
    .then(r => r.text())
    .then(text => {
      const lines = text.split(/\r?\n/);
      if (lines.length < 3) throw "Too few lines in CSV";

      // Combine first two rows of header
      const row1 = lines[0].split(',');
      const row2 = lines[1].split(',');
      const header = row1.map((h,i) => {
        const group = h.trim();
        const sub   = (row2[i]||'').trim();
        return sub ? `${group} ${sub}`.trim() : group;
      });
      const dataCsv = [ header.join(','), ...lines.slice(2) ].join('\n');

      Papa.parse(dataCsv, {
        header: true,
        dynamicTyping: true,
        skipEmptyLines: true,
        complete: function(results) {
          const data = results.data.filter(r =>
            r.Method && r.Method.toString().trim() !== 'Method'
          );
          const fields = results.meta.fields;

          // populate header row
          const $hdr = $('#models-header-row');
          fields.forEach(f => $hdr.append(`<th>${f.trim()}</th>`));

          // index lookups
          const sensorIdx = fields.indexOf('Sensor');
          const repIdx    = fields.indexOf('Representation');
          const yearIdx   = fields.indexOf('Year');
          const monthIdx  = fields.indexOf('Month');

          // representation sort order
          const repOrder = {
            'Monocular':  1, 'Stereo':      2, 'Multiview':   3,
            'Projection': 1, 'Point':       2, 'Voxel':       3, 'Point-Voxel': 4,
            'Early-Fusion': 1, 'Mid-Fusion': 2, 'Intermediate': 3, 'Late-Fusion': 4
          };

          // build columns
          const columns = fields.map((f, idx) => ({
            data: f,
            render: idx === fields.length - 1
              ? d => d ? `<a href="${d.trim()}" target="_blank">Link</a>` : ''
              : undefined
          }));

          // initialize DataTable
          const table = $('#models-table').DataTable({
            data, columns,
            order: [
              [ sensorIdx, 'asc' ],   // Camera → LiDAR → Multi-Modal
              [ repIdx,    'asc' ],   // per repOrder
              [ yearIdx,   'asc' ],   // ascending year
              [ monthIdx,  'asc' ]    // ascending month
            ],
            columnDefs: [
              // custom sort for Representation
              {
                targets: repIdx,
                render: (data, type) =>
                  type === 'sort' ? (repOrder[data] || 99) : data
              },
              // custom sort for Month
              {
                targets: monthIdx,
                render: (data, type) => {
                  if (type === 'sort' || type === 'type') {
                    const map = {
                      Jan:1, Feb:2, Mar:3, Apr:4, May:5, Jun:6,
                      Jul:7, Aug:8, Sep:9, Oct:10, Nov:11, Dec:12
                    };
                    return map[data] || 99;
                  }
                  return data;
                }
              },
              // center AP columns (5–13)
              { targets: Array.from({length:9}, (_,i)=>i+5), className:'dt-center' }
            ]
          });

          // helper: reset filters
          function resetAll() {
            $('#sensor-filters button, #rep-filters button').removeClass('active');
            $('.rep-group').hide();
            table.search('').columns().search('').draw();
          }

          // primary sensor filtering
          $('#sensor-filters button').click(function(){
            resetAll();
            const sensor = $(this).data('sensor');
            $(this).addClass('active');
            if (sensor !== 'All') {
              table.column(sensorIdx)
                   .search('^'+sensor+'$', true, false)
                   .draw();
              $(`.rep-group[data-sensor="${sensor}"]`).show();
            }
          });

          // secondary representation filtering
          $('#rep-filters button').click(function(){
            $('#rep-filters button').removeClass('active');
            $(this).addClass('active');
            const rep = $(this).data('rep');
            table.column(repIdx)
                 .search('^'+rep+'$', true, false)
                 .draw();
          });
        }
      });
    });
});
</script>
