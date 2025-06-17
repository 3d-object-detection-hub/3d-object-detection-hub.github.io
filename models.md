---
layout: default
title: 3D Object Detection
permalink: /models/
---


## All 3D-Object-Detection Models

**Primary filter by sensor:**  
<div id="primary-filters" class="btn-group" style="margin:1em 0;">
  <button data-filter="All">All Models</button>
  <button data-filter="Camera">Camera</button>
  <button data-filter="LiDAR">LiDAR</button>
  <button data-filter="Multi-Modal">Multi-Modal</button>
</div>

<!-- secondary filters: shown only when a specific sensor is selected -->
<div id="secondary-filters" style="margin:0 0 1em;">
  <!-- for Camera -->
  <div class="sensor-specific" data-sensor="Camera" style="display:none;">
    <button data-subfilter="Monocular">Monocular</button>
    <button data-subfilter="Stereo">Stereo</button>
    <button data-subfilter="Multiview">Multiview</button>
  </div>
  <!-- for LiDAR -->
  <div class="sensor-specific" data-sensor="LiDAR" style="display:none;">
    <button data-subfilter="Projection">Projection</button>
    <button data-subfilter="Voxel">Voxel</button>
    <button data-subfilter="Point">Point</button>
    <button data-subfilter="Point-Voxel">Point-Voxel</button>
  </div>
  <!-- for Multi-Modal -->
  <div class="sensor-specific" data-sensor="Multi-Modal" style="display:none;">
    <button data-subfilter="Early-Fusion">Early-Fusion</button>
    <button data-subfilter="Mid-Fusion">Mid-Fusion</button>
    <button data-subfilter="Intermediate">Intermediate</button>
    <button data-subfilter="Late-Fusion">Late-Fusion</button>
  </div>
</div>

<table id="models-table" class="display" style="width:100%">
  <thead>
    <tr>
      <th rowspan="2">Method</th>
      <th rowspan="2">Sensor</th>
      <th rowspan="2">Representation</th>
      <th rowspan="2">Year</th>
      <th rowspan="2">Month</th>
      <th colspan="3">AP2D<br>(KITTI Car)</th>
      <th colspan="3">AP3D<br>(KITTI Car)</th>
      <th colspan="3">APBEV<br>(KITTI Car)</th>
      <th rowspan="2">NuScenes mAP</th>
      <th rowspan="2">NDS</th>
      <th rowspan="2">Waymo L1</th>
      <th rowspan="2">Waymo L2</th>
      <th rowspan="2">Time (s)</th>
      <th rowspan="2">Code</th>
      <th rowspan="2">Hardware</th>
      <th rowspan="2">Paper</th>
    </tr>
    <tr>
      <th>E</th><th>M</th><th>H</th>
      <th>E</th><th>M</th><th>H</th>
      <th>E</th><th>M</th><th>H</th>
    </tr>
  </thead>
</table>

<!-- parameter definitions -->
<div class="table-description" style="margin-top:1.5em; font-size:0.9em; line-height:1.4;">
  <p><strong>Parameter descriptions:</strong></p>
  <ul>
    <li><strong>AP2D:</strong> 2D Average Precision on KITTI Car test (Easy, Moderate, Hard)</li>
    <li><strong>AP3D:</strong> 3D Average Precision on KITTI Car test (Easy, Moderate, Hard)</li>
    <li><strong>APBEV:</strong> Bird’s-Eye-View Average Precision on KITTI Car test (Easy, Moderate, Hard)</li>
    <li><strong>NuScenes mAP:</strong> Mean Average Precision on nuScenes validation set</li>
    <li><strong>NuScenes NDS:</strong> nuScenes Detection Score on validation set</li>
    <li><strong>Waymo L1 / L2:</strong> Level-1 / Level-2 mAP on Waymo Open Dataset validation set</li>
    <li><strong>Time (s):</strong> Inference time per frame (seconds) on the KITTI benchmark</li>
  </ul>
</div>


<script>
$(function(){
  // load and parse CSV
  Papa.parse("{{ '/assets/data/models.csv' | relative_url }}", {
    download: true,
    skipEmptyLines: true,
    header: false,
    complete(results) {
      const data = results.data.slice(2);

      // column definitions
      const cols = [
        { data: 0 },{ data: 1 },{ data: 2 },{ data: 3 },{ data: 4 },
        { data: 5 },{ data: 6 },{ data: 7 },   // AP2D E/M/H
        { data: 8 },{ data: 9 },{ data: 10 },  // AP3D E/M/H
        { data: 11 },{ data: 12 },{ data: 13 },// APBEV E/M/H
        { data: 14 },{ data: 15 },{ data: 16 },{ data: 17 },
        { data: 18 },{ data: 19 },{ data: 20 },
        { data: 21, // Paper URL → Link
          render: v => v ? `<a href="${v.trim()}" target="_blank">Link</a>` : ''
        }
      ];

      const table = $('#models-table').DataTable({
        data, columns: cols,
        pageLength: 25,
        order: [[3,'desc']],
        columnDefs: [
          { targets: [5,6,7,8,9,10,11,12,13], className:'dt-center' }
        ]
      });

      // helper to clear active states & filters
      function clearPrimary() {
        $('#primary-filters button').removeClass('active');
        table.column(1).search('').draw();
        $('#secondary-filters .sensor-specific').hide();
        $('#secondary-filters button').removeClass('active');
        table.column(2).search('');
      }
      function clearSecondary() {
        $('#secondary-filters button').removeClass('active');
        table.column(2).search('').draw();
      }

      // primary sensor filtering
      $('#primary-filters button').click(function(){
        clearPrimary();
        const sensor = $(this).data('filter');
        $(this).addClass('active');
        if (sensor !== 'All') {
          table.column(1)
               .search('^'+sensor+'$', true, false)
               .draw();
          // show corresponding secondary row
          $(`#secondary-filters .sensor-specific[data-sensor="${sensor}"]`).show();
        }
      });

      // secondary representation filtering (within chosen sensor)
      $('#secondary-filters button').click(function(){
        clearSecondary();
        const rep = $(this).data('subfilter');
        $(this).addClass('active');
        table.column(2)
             .search('^'+rep+'$', true, false)
             .draw();
      });
    }
  });
});
</script>
