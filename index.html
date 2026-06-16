<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Fissure - Graphe exploité</title>
  <style>
    :root{
      --bg:#f4f7fb; --card:#fff; --text:#1f2937; --muted:#6b7280; --primary:#1d4ed8;
      --primary-dark:#163ea8; --border:#dbe3ee; --ok:#15803d; --warn:#b45309; --bad:#b91c1c;
      --shadow:0 10px 25px rgba(0,0,0,.08); --radius:16px;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Segoe UI,Tahoma,sans-serif;background:linear-gradient(180deg,#eef4ff 0%,var(--bg) 100%);color:var(--text)}
    header{background:linear-gradient(135deg,#0f172a,#1d4ed8);color:#fff;text-align:center;padding:28px 18px}
    header h1{margin:0 0 8px;font-size:2rem}
    header p{margin:0;max-width:980px;margin-inline:auto;line-height:1.6;opacity:.96}
    main{width:min(1320px,95%);margin:22px auto 40px}
    .card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);box-shadow:var(--shadow);padding:20px;margin-bottom:20px}
    h2{margin-top:0}
    .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:14px}
    .field{display:flex;flex-direction:column;gap:6px}
    .field label{font-weight:600;color:#111827}
    .field input,.field select{padding:10px 12px;border:1px solid #cbd5e1;border-radius:10px;font-size:.95rem;background:#fff}
    .actions{display:flex;flex-wrap:wrap;gap:12px;margin-top:16px}
    button{border:none;border-radius:12px;padding:11px 16px;font-weight:700;cursor:pointer;transition:.2s ease}
    .btn-primary{background:var(--primary);color:#fff}.btn-primary:hover{background:var(--primary-dark)}
    .btn-secondary{background:#e5e7eb;color:#111827}.btn-secondary:hover{background:#d1d5db}
    .hint{font-size:.93rem;color:var(--muted);line-height:1.6;margin-top:12px}
    .result{margin-top:14px;padding:14px;border-left:5px solid var(--primary);border-radius:12px;background:#f8fbff;white-space:pre-line;line-height:1.65}
    .status{display:inline-block;margin-top:10px;padding:6px 12px;border-radius:999px;font-size:.88rem;font-weight:700}
    .ok{background:#dcfce7;color:var(--ok)}.warn{background:#fef3c7;color:var(--warn)}.bad{background:#fee2e2;color:var(--bad)}
    .canvas-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(320px,1fr));gap:16px;margin-top:16px}
    .canvas-wrap{background:#fff;border:1px solid var(--border);border-radius:14px;padding:12px}
    .canvas-wrap h3{margin:0 0 10px;font-size:1rem}
    .canvas-wrap.active-calibration{border:2px solid #1d4ed8;box-shadow:0 0 0 4px rgba(29,78,216,.12)}
    canvas{width:100%;background:#fff;border-radius:10px;border:1px solid #e5e7eb;display:block}
    .small{font-size:.9rem;color:var(--muted);margin-top:8px;line-height:1.5}
    code{background:#eef2ff;padding:2px 6px;border-radius:6px}
    @media print {
      body{background:#fff}
      .actions, #imageInput, button{display:none!important}
      .card{box-shadow:none}
    }
  </style>
</head>
<body>
  <header>
    <h1>Mesure automatique de fissure en mm et contrainte en MPa</h1>
    <p>Cette version exploite les résultats directement dans le graphe : zones de sécurité, seuil critique, point mesuré annoté et interprétation automatique.</p>
  </header>

  <main>
    <section class="card">
      <h2>1. Chargement et paramètres image</h2>
      <div class="grid">
        <div class="field">
          <label for="imageInput">Photo de la fissure</label>
          <input id="imageInput" type="file" accept="image/*" />
        </div>

        <div class="field">
          <label for="mmPerPixel">Échelle (mm/pixel)</label>
          <input id="mmPerPixel" type="number" step="any" value="" placeholder="Détection auto ou calibration" />
        </div>

        <div class="field">
          <label for="knownScaleMm">Longueur réelle du repère auto (mm)</label>
          <input id="knownScaleMm" type="number" step="any" value="10" />
        </div>

        <div class="field">
          <label for="autoScaleZone">Zone de recherche du repère</label>
          <select id="autoScaleZone">
            <option value="bottom" selected>Bas de l’image</option>
            <option value="full">Toute l’image</option>
          </select>
        </div>

        <div class="field">
          <label for="realDistanceMm">Distance réelle de référence (mm)</label>
          <input id="realDistanceMm" type="number" step="any" value="10" />
        </div>

        <div class="field">
          <label for="criticalStress">Seuil critique graphe (MPa)</label>
          <input id="criticalStress" type="number" step="any" value="3" />
        </div>

        <div class="field">
          <label for="blurSize">Flou gaussien</label>
          <input id="blurSize" type="number" step="2" value="5" />
        </div>

        <div class="field">
          <label for="blockSize">Seuil adaptatif (taille bloc)</label>
          <input id="blockSize" type="number" step="2" value="31" />
        </div>

        <div class="field">
          <label for="cValue">Seuil adaptatif (C)</label>
          <input id="cValue" type="number" step="any" value="8" />
        </div>

        <div class="field">
          <label for="minArea">Aire minimale à conserver (px²)</label>
          <input id="minArea" type="number" step="1" value="80" />
        </div>
      </div>

      <div class="actions">
        <button class="btn-primary" id="processBtn">Détecter la fissure</button>
        <button class="btn-secondary" id="autoScaleBtn">Détecter l’échelle auto</button>
        <button class="btn-secondary" id="calibrateBtn">Calibrer par 2 points</button>
        <button class="btn-secondary" id="resetBtn">Réinitialiser</button>
      </div>

      <div id="calibrationInfo" class="result">Aucune calibration active.</div>
    </section>

    <section class="card">
      <h2>2. Paramètres mécaniques</h2>
      <div class="grid">
        <div class="field"><label for="youngE">Module de Young E (GPa)</label><input id="youngE" type="number" step="any" value="30" /></div>
        <div class="field"><label for="gamma">Énergie spécifique γ (J/m²)</label><input id="gamma" type="number" step="any" value="1" /></div>
        <div class="field"><label for="kic">Ténacité critique K<sub>Ic</sub> (MPa√m)</label><input id="kic" type="number" step="any" value="1" /></div>
        <div class="field"><label for="geomY">Facteur géométrique Y</label><input id="geomY" type="number" step="any" value="1.12" /></div>
      </div>
      <p class="hint">Formules : <code>σc = √((2Eγ)/(πa))</code> et <code>σc = K<sub>Ic</sub> / (Y√(πa))</code>, avec <code>a = L/2</code>.</p>
    </section>

    <section class="card">
      <h2>3. Résultats numériques</h2>
      <div id="report" class="result">Aucune analyse effectuée.</div>
      <div id="graphSummary" class="result">L’interprétation du graphe apparaîtra ici après traitement.</div>
    </section>

    <section class="card">
      <h2>4. Résultats visuels</h2>
      <div class="canvas-grid">
        <div class="canvas-wrap" id="originalWrap">
          <h3>Image originale</h3>
          <canvas id="canvasOriginal" width="520" height="380"></canvas>
          <div class="small">En mode calibration, clique 2 points sur cette image.</div>
        </div>
        <div class="canvas-wrap">
          <h3>Masque binaire</h3>
          <canvas id="canvasMask" width="520" height="380"></canvas>
          <div class="small">Détection automatique de la fissure.</div>
        </div>
        <div class="canvas-wrap">
          <h3>Résultat annoté</h3>
          <canvas id="canvasResult" width="520" height="380"></canvas>
          <div class="small">Contour, boîte, largeur, longueur, et repère éventuel.</div>
        </div>
      </div>
    </section>

    <section class="card">
      <h2>5. Diagnostic automatique</h2>
      <div id="diagnosticText" class="result">Le diagnostic apparaîtra ici après traitement.</div>
      <div id="typeText" class="result" style="margin-top:12px;">Le type probable de fissure apparaîtra ici après traitement.</div>
    </section>

    <section class="card">
      <h2>6. Exploitation graphique fissure / contrainte</h2>
      <canvas id="chartCanvas" width="900" height="360"></canvas>
      <div class="small">Le graphe affiche maintenant : zone sûre, zone de surveillance, zone critique, seuil horizontal et point mesuré annoté.</div>
      <div class="actions">
        <button class="btn-primary" id="printBtn">Exporter en PDF</button>
      </div>
    </section>
  </main>

  <img id="hiddenImage" alt="source" style="display:none;" />
  <script async src="https://docs.opencv.org/4.x/opencv.js"></script>
  <script>
    let sourceImageLoaded = false;
    let cvReady = false;
    let currentFile = null;
    let calibrationMode = false;
    let calibrationPoints = [];
    let lastAutoScaleDetection = null;

    const imageInput = document.getElementById('imageInput');
    const processBtn = document.getElementById('processBtn');
    const resetBtn = document.getElementById('resetBtn');
    const calibrateBtn = document.getElementById('calibrateBtn');
    const autoScaleBtn = document.getElementById('autoScaleBtn');
    const hiddenImage = document.getElementById('hiddenImage');
    const report = document.getElementById('report');
    const graphSummary = document.getElementById('graphSummary');
    const diagnosticText = document.getElementById('diagnosticText');
    const typeText = document.getElementById('typeText');
    const calibrationInfo = document.getElementById('calibrationInfo');
    const realDistanceMmInput = document.getElementById('realDistanceMm');
    const knownScaleMmInput = document.getElementById('knownScaleMm');
    const autoScaleZone = document.getElementById('autoScaleZone');
    const criticalStressInput = document.getElementById('criticalStress');
    const canvasOriginal = document.getElementById('canvasOriginal');
    const canvasMask = document.getElementById('canvasMask');
    const canvasResult = document.getElementById('canvasResult');
    const chartCanvas = document.getElementById('chartCanvas');
    const printBtn = document.getElementById('printBtn');
    const originalWrap = document.getElementById('originalWrap');

    function setReport(text, statusClass='') {
      report.innerHTML = text + (statusClass ? `\n<div class="status ${statusClass}">${statusClass === 'ok' ? 'Analyse réussie' : statusClass === 'warn' ? 'Résultat indicatif' : 'Erreur'}</div>` : '');
    }
    function setGraphSummary(text, statusClass='') {
      graphSummary.innerHTML = text + (statusClass ? `\n<div class="status ${statusClass}">${statusClass === 'ok' ? 'Lecture du graphe' : statusClass === 'warn' ? 'Lecture indicative' : 'Lecture indisponible'}</div>` : '');
    }
    function setDiagnostic(text, statusClass='') {
      diagnosticText.innerHTML = text + (statusClass ? `\n<div class="status ${statusClass}">${statusClass === 'ok' ? 'Diagnostic rassurant' : statusClass === 'warn' ? 'Surveillance conseillée' : 'Expertise recommandée'}</div>` : '');
    }
    function setType(text, statusClass='') {
      typeText.innerHTML = text + (statusClass ? `\n<div class="status ${statusClass}">${statusClass === 'ok' ? 'Type probable identifié' : statusClass === 'warn' ? 'Interprétation indicative' : 'Interprétation incertaine'}</div>` : '');
    }
    function setCalibrationInfo(text, status='warn') {
      calibrationInfo.innerHTML = text + `<div class="status ${status}">${status === 'ok' ? 'Calibration active' : status === 'bad' ? 'Calibration invalide' : 'Calibration en attente'}</div>`;
    }

    function resetCanvases(){
      [canvasOriginal, canvasMask, canvasResult].forEach(c => {
        const ctx = c.getContext('2d');
        ctx.clearRect(0,0,c.width,c.height);
        ctx.fillStyle = '#fff';
        ctx.fillRect(0,0,c.width,c.height);
      });
    }
    function drawImageFit(img, canvas){
      const ctx = canvas.getContext('2d');
      ctx.clearRect(0,0,canvas.width,canvas.height);
      ctx.fillStyle = '#fff';
      ctx.fillRect(0,0,canvas.width,canvas.height);
      const scale = Math.min(canvas.width/img.width, canvas.height/img.height);
      const w = img.width * scale, h = img.height * scale;
      const x = (canvas.width - w)/2, y = (canvas.height - h)/2;
      ctx.drawImage(img, x, y, w, h);
    }
    function getDisplayedImageRect(img, canvas){
      const scale = Math.min(canvas.width / img.width, canvas.height / img.height);
      const w = img.width * scale;
      const h = img.height * scale;
      const x = (canvas.width - w) / 2;
      const y = (canvas.height - h) / 2;
      return {x, y, w, h, scale};
    }

    function redrawOriginalWithCalibration(){
      if(!hiddenImage.src) return;
      drawImageFit(hiddenImage, canvasOriginal);
      const ctx = canvasOriginal.getContext('2d');
      const rect = getDisplayedImageRect(hiddenImage, canvasOriginal);

      if(lastAutoScaleDetection){
        const d = lastAutoScaleDetection;
        ctx.save();
        ctx.strokeStyle = '#2563eb';
        ctx.lineWidth = 3;
        ctx.beginPath();
        ctx.moveTo(rect.x + d.x1 * rect.scale, rect.y + d.y1 * rect.scale);
        ctx.lineTo(rect.x + d.x2 * rect.scale, rect.y + d.y2 * rect.scale);
        ctx.stroke();
        ctx.fillStyle = '#2563eb';
        ctx.font = '12px Segoe UI';
        ctx.fillText('Repère auto', rect.x + d.x1 * rect.scale + 6, rect.y + d.y1 * rect.scale - 6);
        ctx.restore();
      }

      if(calibrationPoints.length > 0){
        ctx.save();
        ctx.lineWidth = 2;
        ctx.strokeStyle = '#dc2626';
        ctx.fillStyle = '#dc2626';
        ctx.font = '14px Segoe UI';

        calibrationPoints.forEach((p, idx) => {
          const px = rect.x + p.x * rect.scale;
          const py = rect.y + p.y * rect.scale;
          ctx.beginPath();
          ctx.arc(px, py, 5, 0, 2*Math.PI);
          ctx.fill();
          ctx.fillText(String(idx + 1), px + 8, py - 8);
        });

        if(calibrationPoints.length === 2){
          const p1 = calibrationPoints[0];
          const p2 = calibrationPoints[1];
          const x1 = rect.x + p1.x * rect.scale;
          const y1 = rect.y + p1.y * rect.scale;
          const x2 = rect.x + p2.x * rect.scale;
          const y2 = rect.y + p2.y * rect.scale;
          ctx.beginPath();
          ctx.moveTo(x1, y1);
          ctx.lineTo(x2, y2);
          ctx.stroke();
        }
        ctx.restore();
      }
    }

    function startCalibrationMode(){
      if(!sourceImageLoaded){
        setCalibrationInfo('Charge une image avant de lancer la calibration.', 'bad');
        return;
      }
      calibrationMode = true;
      calibrationPoints = [];
      originalWrap.classList.add('active-calibration');
      setCalibrationInfo('Calibration active : clique deux points sur l’image correspondant à une distance réelle connue.', 'warn');
      redrawOriginalWithCalibration();
    }
    function stopCalibrationMode(){
      calibrationMode = false;
      originalWrap.classList.remove('active-calibration');
    }
    function finalizeCalibration(){
      if(calibrationPoints.length !== 2){
        setCalibrationInfo('Deux points sont nécessaires pour calculer l’échelle.', 'bad');
        return;
      }
      const realDistanceMm = parseFloat(realDistanceMmInput.value);
      if(!Number.isFinite(realDistanceMm) || realDistanceMm <= 0){
        setCalibrationInfo('La distance réelle doit être strictement positive.', 'bad');
        return;
      }
      const [p1, p2] = calibrationPoints;
      const pixelDistance = Math.hypot(p2.x - p1.x, p2.y - p1.y);
      if(pixelDistance <= 0){
        setCalibrationInfo('Distance en pixels invalide.', 'bad');
        return;
      }
      const mmPerPixel = realDistanceMm / pixelDistance;
      document.getElementById('mmPerPixel').value = mmPerPixel.toFixed(6);
      setCalibrationInfo(`Calibration manuelle réussie.\n\nDistance réelle : ${realDistanceMm.toFixed(3)} mm\nDistance image : ${pixelDistance.toFixed(2)} px\nÉchelle calculée : ${mmPerPixel.toFixed(6)} mm/pixel`, 'ok');
      stopCalibrationMode();
      redrawOriginalWithCalibration();
    }

    function toOdd(v,fallback){
      v = parseInt(v,10);
      if(!Number.isFinite(v) || v < 3) return fallback;
      return v % 2 === 0 ? v + 1 : v;
    }
    function clamp(v, min, max) { return Math.min(Math.max(v, min), max); }

    function autoImageParams(img) {
      const w = img.naturalWidth || img.width;
      const h = img.naturalHeight || img.height;
      const maxDim = Math.max(w, h);
      let blurSize = Math.round(maxDim / 300);
      if (blurSize < 3) blurSize = 3;
      if (blurSize % 2 === 0) blurSize += 1;
      blurSize = clamp(blurSize, 3, 11);

      let blockSize = Math.round(maxDim / 40);
      if (blockSize < 15) blockSize = 15;
      if (blockSize % 2 === 0) blockSize += 1;
      blockSize = clamp(blockSize, 15, 101);

      let cValue = 8;
      if (maxDim < 800) cValue = 5;
      else if (maxDim < 1600) cValue = 7;
      else cValue = 9;

      let minArea = Math.round((w * h) * 0.00005);
      minArea = clamp(minArea, 20, 500);
      return { width:w, height:h, blurSize, blockSize, cValue, minArea };
    }

    function applyAutoParamsFromImage(img) {
      const p = autoImageParams(img);
      document.getElementById('blurSize').value = p.blurSize;
      document.getElementById('blockSize').value = p.blockSize;
      document.getElementById('cValue').value = p.cValue;
      document.getElementById('minArea').value = p.minArea;
      const mmInput = document.getElementById('mmPerPixel');
      if (!mmInput.value || parseFloat(mmInput.value) <= 0) {
        mmInput.value = '';
        mmInput.placeholder = 'Détection auto ou calibration';
      }
      setReport(
        `Photo chargée automatiquement.\n\nDimensions image : ${p.width} × ${p.height} px\nParamètres proposés automatiquement :\n- Flou gaussien : ${p.blurSize}\n- Taille bloc : ${p.blockSize}\n- C : ${p.cValue}\n- Aire minimale : ${p.minArea} px²`,
        'ok'
      );
    }

    function detectScaleMarkerAuto(){
      if(!cvReady || !sourceImageLoaded) return {found:false, reason:'Image ou OpenCV indisponible.'};
      const knownScaleMm = parseFloat(knownScaleMmInput.value);
      if(!Number.isFinite(knownScaleMm) || knownScaleMm <= 0) return {found:false, reason:'La longueur réelle du repère doit être > 0.'};

      let src=null, gray=null, roi=null, edges=null, lines=null;
      try{
        src = cv.imread(hiddenImage);
        gray = new cv.Mat();
        cv.cvtColor(src, gray, cv.COLOR_RGBA2GRAY);

        let searchY = 0, searchH = gray.rows;
        if(autoScaleZone.value === 'bottom'){
          searchY = Math.floor(gray.rows * 0.65);
          searchH = gray.rows - searchY;
        }

        roi = gray.roi(new cv.Rect(0, searchY, gray.cols, searchH));
        let blur = new cv.Mat();
        cv.GaussianBlur(roi, blur, new cv.Size(5,5), 0, 0, cv.BORDER_DEFAULT);
        edges = new cv.Mat();
        cv.Canny(blur, edges, 50, 150, 3, false);

        lines = new cv.Mat();
        cv.HoughLinesP(edges, lines, 1, Math.PI/180, 45, Math.max(40, Math.round(gray.cols * 0.08)), 12);

        let best = null;
        for(let i=0; i<lines.rows; i++){
          const l = lines.data32S.slice(i*4, i*4+4);
          let [x1,y1,x2,y2] = l;
          y1 += searchY; y2 += searchY;
          const dx = x2 - x1, dy = y2 - y1;
          const len = Math.hypot(dx, dy);
          if(len < 30) continue;
          const angle = Math.abs(Math.atan2(dy, dx) * 180 / Math.PI);
          const horiz = Math.min(angle, Math.abs(180 - angle));
          if(horiz > 12) continue;
          const centerY = (y1 + y2) / 2;
          const bottomPreference = autoScaleZone.value === 'bottom' ? centerY / gray.rows : 0.5;
          const score = len + bottomPreference * 50;
          if(!best || score > best.score) best = {x1,y1,x2,y2,lengthPx:len,score};
        }
        blur.delete();
        if(!best) return {found:false, reason:'Aucun repère linéaire exploitable détecté.'};

        const mmPerPixel = knownScaleMm / best.lengthPx;
        return {found:true, mmPerPixel, details:`Repère horizontal détecté : ${best.lengthPx.toFixed(2)} px pour ${knownScaleMm.toFixed(2)} mm.`, x1:best.x1, y1:best.y1, x2:best.x2, y2:best.y2, lengthPx:best.lengthPx};
      } catch(err){
        return {found:false, reason:'Erreur auto-échelle : ' + err};
      } finally {
        if(src) src.delete();
        if(gray) gray.delete();
        if(roi) roi.delete();
        if(edges) edges.delete();
        if(lines) lines.delete();
      }
    }

    function applyAutoScaleDetection(showMessage=true){
      const auto = detectScaleMarkerAuto();
      if(auto.found && Number.isFinite(auto.mmPerPixel) && auto.mmPerPixel > 0){
        document.getElementById('mmPerPixel').value = auto.mmPerPixel.toFixed(6);
        lastAutoScaleDetection = auto;
        redrawOriginalWithCalibration();
        if(showMessage) setCalibrationInfo(`Échelle détectée automatiquement.\n\n${auto.details}\nÉchelle calculée : ${auto.mmPerPixel.toFixed(6)} mm/pixel`, 'ok');
      } else {
        lastAutoScaleDetection = null;
        redrawOriginalWithCalibration();
        if(showMessage) setCalibrationInfo(`Détection automatique impossible.\n${auto.reason || 'Aucun repère trouvé.'}\nUtilise la calibration manuelle par 2 points si besoin.`, 'warn');
      }
    }

    function computeContourLength(cnt){
      let length = 0;
      const rows = cnt.data32S.length/2;
      for(let i=1;i<rows;i++){
        const x1=cnt.data32S[(i-1)*2], y1=cnt.data32S[(i-1)*2+1], x2=cnt.data32S[i*2], y2=cnt.data32S[i*2+1];
        length += Math.hypot(x2-x1,y2-y1);
      }
      return length;
    }

    function cleanByArea(binary,minArea){
      let labels=new cv.Mat(), stats=new cv.Mat(), centroids=new cv.Mat();
      const n=cv.connectedComponentsWithStats(binary,labels,stats,centroids,8,cv.CV_32S);
      let cleaned=cv.Mat.zeros(binary.rows,binary.cols,cv.CV_8UC1);
      for(let label=1;label<n;label++){
        const area=stats.intAt(label,cv.CC_STAT_AREA);
        if(area>=minArea){
          for(let y=0;y<labels.rows;y++){
            for(let x=0;x<labels.cols;x++){
              if(labels.intAt(y,x)===label) cleaned.ucharPtr(y,x)[0]=255;
            }
          }
        }
      }
      labels.delete(); stats.delete(); centroids.delete();
      return cleaned;
    }

    function distanceTransformWidthEstimate(binaryMat){
      let dist=new cv.Mat();
      cv.distanceTransform(binaryMat,dist,cv.DIST_L2,3);
      let values=[];
      for(let y=0;y<dist.rows;y++){
        for(let x=0;x<dist.cols;x++){
          const d=dist.floatAt(y,x);
          if(d>0.5) values.push(d);
        }
      }
      dist.delete();
      if(values.length===0) return {meanWidthPx:0, medianWidthPx:0, maxWidthPx:0};
      values.sort((a,b)=>a-b);
      const meanRadius=values.reduce((s,v)=>s+v,0)/values.length;
      const medianRadius=values[Math.floor(values.length/2)];
      const maxRadius=values[values.length-1];
      return {meanWidthPx:2*meanRadius, medianWidthPx:2*medianRadius, maxWidthPx:2*maxRadius};
    }

    function diagnosticFissure(w_mm, sigma_MPa){
      let texte='', status='ok';
      if(w_mm<=0.3){ texte='Comparaison technique :\n- Ouverture ≤ 0.3 mm.\n- Fissure fine, généralement admissible si elle reste stable.'; status='ok'; }
      else if(w_mm<=1.0){ texte='Comparaison technique :\n- 0.3 mm < ouverture ≤ 1.0 mm.\n- Fissure modérée, surveillance conseillée.'; status='warn'; }
      else { texte='Comparaison technique :\n- Ouverture > 1.0 mm.\n- Fissure importante, expertise recommandée.'; status='bad'; }

      if(Number.isFinite(sigma_MPa)){
        texte += '\n\nAnalyse mécanique :\n' + (sigma_MPa > 5 ? '- La contrainte critique théorique est élevée.' : '- La contrainte critique théorique reste modérée.');
      }
      return {texte,status};
    }

    function classifyCrackType(rect, lengthMm, maxWidthMm){
      if(!rect) return {texte:'Type probable : non déterminé.', status:'bad'};
      const ratio = rect.width > rect.height ? rect.width / Math.max(rect.height, 1) : rect.height / Math.max(rect.width, 1);
      const orientation = rect.width >= rect.height ? 'horizontale' : 'verticale';
      let texte = 'Type probable de fissure :\n';
      let status = 'warn';

      if(ratio >= 4 && orientation === 'verticale'){ texte += '- Morphologie verticale et allongée.'; status = 'ok'; }
      else if(ratio >= 4 && orientation === 'horizontale'){ texte += '- Morphologie horizontale et allongée.'; status = 'ok'; }
      else if(ratio < 4 && ratio >= 1.5){ texte += '- Morphologie oblongue, peu directionnelle.'; status = 'warn'; }
      else { texte += '- Forme diffuse ou ramifiée.'; status = 'warn'; }

      if(Number.isFinite(lengthMm) && Number.isFinite(maxWidthMm)){
        texte += `\n\nLongueur : ${lengthMm.toFixed(2)} mm\nLargeur max : ${maxWidthMm.toFixed(3)} mm`;
      }
      return {texte, status};
    }

    function interpretGraph(sigmaIrwin_MPa, criticalStress){
      if(!Number.isFinite(sigmaIrwin_MPa)) return {label:'Interprétation impossible', status:'warn'};
      if(sigmaIrwin_MPa >= criticalStress * 1.5) return {label:'Zone sûre', status:'ok'};
      if(sigmaIrwin_MPa >= criticalStress) return {label:'Zone de surveillance', status:'warn'};
      return {label:'Zone critique', status:'bad'};
    }

    function drawComparisonChart(a, sigmaGriffith_MPa, sigmaIrwin_MPa, E_GPa, gamma, KIc_MPa, Y, criticalStress){
      const ctx = chartCanvas.getContext('2d');
      const w = chartCanvas.width, h = chartCanvas.height;
      ctx.clearRect(0,0,w,h);
      ctx.fillStyle='#fff';
      ctx.fillRect(0,0,w,h);

      const padL=70, padR=20, padT=25, padB=50;
      const plotW=w-padL-padR, plotH=h-padT-padB;

      const aMin=Math.max(a/10,1e-6), aMax=Math.max(a*3,aMin*2), N=120;
      const xs=[], yg=[], yi=[], E=E_GPa*1e9, KIc=KIc_MPa*1e6;
      for(let i=0;i<N;i++){
        const aa=aMin+(aMax-aMin)*i/(N-1);
        xs.push(aa);
        yg.push(Math.sqrt((2*E*gamma)/(Math.PI*aa))/1e6);
        yi.push((KIc/(Y*Math.sqrt(Math.PI*aa)))/1e6);
      }
      const yMax=Math.max(...yg,...yi,sigmaGriffith_MPa||0,sigmaIrwin_MPa||0,criticalStress||0)*1.15;
      const mapX=x=>padL+(x-aMin)/(aMax-aMin)*plotW;
      const mapY=y=>h-padB-(y/Math.max(yMax,1e-6))*plotH;

      const safeLimit = Math.max(criticalStress * 1.5, yMax * 0.7);
      const warnLimit = Math.max(criticalStress, yMax * 0.4);

      ctx.fillStyle = "rgba(34,197,94,0.15)";
      ctx.fillRect(padL, mapY(yMax), plotW, mapY(safeLimit) - mapY(yMax));
      ctx.fillStyle = "rgba(234,179,8,0.15)";
      ctx.fillRect(padL, mapY(safeLimit), plotW, mapY(warnLimit) - mapY(safeLimit));
      ctx.fillStyle = "rgba(220,38,38,0.15)";
      ctx.fillRect(padL, mapY(warnLimit), plotW, mapY(0) - mapY(warnLimit));

      ctx.strokeStyle='#cbd5e1';
      ctx.lineWidth=1;
      for(let i=0;i<=5;i++){
        const y=padT+i*plotH/5;
        ctx.beginPath(); ctx.moveTo(padL,y); ctx.lineTo(w-padR,y); ctx.stroke();
      }

      ctx.beginPath();
      ctx.moveTo(padL,padT);
      ctx.lineTo(padL,h-padB);
      ctx.lineTo(w-padR,h-padB);
      ctx.strokeStyle='#111827';
      ctx.lineWidth=2;
      ctx.stroke();

      ctx.fillStyle='#111827';
      ctx.font='bold 16px Segoe UI';
      ctx.fillText('Exploitation du graphe contrainte / demi-longueur', padL, 18);
      ctx.font='12px Segoe UI';
      ctx.fillText('a (m)', w-45, h-15);
      ctx.save();
      ctx.translate(18, h/2);
      ctx.rotate(-Math.PI/2);
      ctx.fillText('σc (MPa)', 0, 0);
      ctx.restore();

      ctx.fillStyle='#15803d';
      ctx.fillText('Zone sûre', w-130, 70);
      ctx.fillStyle='#b45309';
      ctx.fillText('Surveillance', w-130, 95);
      ctx.fillStyle='#b91c1c';
      ctx.fillText('Critique', w-130, 120);

      ctx.strokeStyle='#1d4ed8';
      ctx.lineWidth=2;
      ctx.beginPath();
      ctx.moveTo(mapX(xs[0]),mapY(yg[0]));
      for(let i=1;i<N;i++) ctx.lineTo(mapX(xs[i]),mapY(yg[i]));
      ctx.stroke();

      ctx.strokeStyle='#15803d';
      ctx.beginPath();
      ctx.moveTo(mapX(xs[0]),mapY(yi[0]));
      for(let i=1;i<N;i++) ctx.lineTo(mapX(xs[i]),mapY(yi[i]));
      ctx.stroke();

      ctx.strokeStyle='#dc2626';
      ctx.setLineDash([6,5]);
      ctx.beginPath();
      ctx.moveTo(padL, mapY(criticalStress));
      ctx.lineTo(w-padR, mapY(criticalStress));
      ctx.stroke();
      ctx.setLineDash([]);
      ctx.fillStyle='#dc2626';
      ctx.fillText(`Seuil ${criticalStress.toFixed(2)} MPa`, padL + 8, mapY(criticalStress) - 6);

      if(Number.isFinite(sigmaIrwin_MPa)){
        ctx.fillStyle='#dc2626';
        ctx.beginPath();
        ctx.arc(mapX(a), mapY(sigmaIrwin_MPa), 5, 0, 2*Math.PI);
        ctx.fill();

        ctx.font='12px Segoe UI';
        ctx.fillText(`${sigmaIrwin_MPa.toFixed(2)} MPa`, mapX(a) + 8, mapY(sigmaIrwin_MPa) - 8);

        ctx.strokeStyle='#111827';
        ctx.lineWidth=1.5;
        ctx.beginPath();
        ctx.moveTo(mapX(a), mapY(sigmaIrwin_MPa));
        ctx.lineTo(mapX(Math.min(a*1.35, aMax)), mapY(Math.max(sigmaIrwin_MPa*0.75, 0)));
        ctx.stroke();
      }

      ctx.fillStyle='#111827';
      ctx.fillText(aMin.toExponential(2), padL-10, h-28);
      ctx.fillText(aMax.toExponential(2), w-85, h-28);
      ctx.fillText('0', 52, h-padB+4);
      ctx.fillText(yMax.toFixed(2), 24, padT+5);

      ctx.fillStyle='#1d4ed8';
      ctx.fillRect(w-250, 35, 14, 3);
      ctx.fillStyle='#111827';
      ctx.fillText('Griffith', w-230, 40);

      ctx.fillStyle='#15803d';
      ctx.fillRect(w-160, 35, 14, 3);
      ctx.fillStyle='#111827';
      ctx.fillText('Irwin', w-140, 40);

      ctx.fillStyle='#dc2626';
      ctx.beginPath();
      ctx.arc(w-80, 38, 4, 0, 2*Math.PI);
      ctx.fill();
      ctx.fillStyle='#111827';
      ctx.fillText('Mesure', w-68, 42);
    }

    function detectCrackAndCompute(){
      if(!cvReady){ setReport("OpenCV.js n’est pas encore chargé.",'bad'); return; }
      if(!sourceImageLoaded){ setReport("Charge d’abord une photo.",'bad'); return; }

      try{
        const mmPerPixel=parseFloat(document.getElementById('mmPerPixel').value);
        const blurSize=toOdd(document.getElementById('blurSize').value,5);
        const blockSize=toOdd(document.getElementById('blockSize').value,31);
        const cValue=parseFloat(document.getElementById('cValue').value)||8;
        const minArea=parseFloat(document.getElementById('minArea').value)||80;
        const criticalStress=parseFloat(criticalStressInput.value)||3;
        const E_GPa=parseFloat(document.getElementById('youngE').value);
        const gamma=parseFloat(document.getElementById('gamma').value);
        const KIc_MPa=parseFloat(document.getElementById('kic').value);
        const Y=parseFloat(document.getElementById('geomY').value);
        const E=E_GPa*1e9, KIc=KIc_MPa*1e6;

        let src=cv.imread(canvasOriginal), gray=new cv.Mat(), blur=new cv.Mat(), thresh=new cv.Mat(), morph=new cv.Mat();
        cv.cvtColor(src,gray,cv.COLOR_RGBA2GRAY);
        cv.GaussianBlur(gray,blur,new cv.Size(blurSize,blurSize),0,0,cv.BORDER_DEFAULT);
        cv.adaptiveThreshold(blur,thresh,255,cv.ADAPTIVE_THRESH_GAUSSIAN_C,cv.THRESH_BINARY_INV,blockSize,cValue);
        const kernel=cv.getStructuringElement(cv.MORPH_ELLIPSE,new cv.Size(3,3));
        cv.morphologyEx(thresh,morph,cv.MORPH_OPEN,kernel);
        cv.morphologyEx(morph,morph,cv.MORPH_CLOSE,kernel);

        let cleaned=cleanByArea(morph,minArea);
        cv.imshow('canvasMask',cleaned);

        let contours=new cv.MatVector(), hierarchy=new cv.Mat();
        cv.findContours(cleaned,contours,hierarchy,cv.RETR_EXTERNAL,cv.CHAIN_APPROX_SIMPLE);
        let result=src.clone(), bestIndex=-1, bestArea=0, bestRect=null;

        for(let i=0;i<contours.size();i++){
          const cnt=contours.get(i), area=cv.contourArea(cnt);
          if(area>bestArea){ bestArea=area; bestIndex=i; bestRect=cv.boundingRect(cnt); }
          cnt.delete();
        }

        if(bestIndex===-1||!bestRect){
          cv.imshow('canvasResult',result);
          setReport('Aucune fissure claire n’a été détectée. Essaie une photo plus nette ou ajuste les paramètres.','warn');
          setDiagnostic('Impossible de formuler un diagnostic fiable car la fissure n’a pas été détectée correctement sur l’image.','warn');
          setType('Type probable : indéterminé.', 'bad');
          setGraphSummary('Le graphe ne peut pas être exploité sans fissure détectée.', 'bad');
          src.delete();gray.delete();blur.delete();thresh.delete();morph.delete();cleaned.delete();contours.delete();hierarchy.delete();result.delete();kernel.delete();
          return;
        }

        let crackMask=cv.Mat.zeros(cleaned.rows,cleaned.cols,cv.CV_8UC1);
        let contours2=new cv.MatVector(), hierarchy2=new cv.Mat();
        cv.findContours(cleaned,contours2,hierarchy2,cv.RETR_EXTERNAL,cv.CHAIN_APPROX_SIMPLE);
        let selectedContour=null;
        for(let i=0;i<contours2.size();i++){
          const cnt=contours2.get(i), area=cv.contourArea(cnt);
          if(i===bestIndex||area===bestArea){
            cv.drawContours(crackMask,contours2,i,new cv.Scalar(255,255,255,255),-1);
            selectedContour=cnt.clone();
          }
          cnt.delete();
        }

        const widths=distanceTransformWidthEstimate(crackMask);
        const crackLengthPx=selectedContour?computeContourLength(selectedContour):0;
        const lengthMm=Number.isFinite(mmPerPixel)&&mmPerPixel>0?crackLengthPx*mmPerPixel:NaN;
        const meanWidthMm=Number.isFinite(mmPerPixel)&&mmPerPixel>0?widths.meanWidthPx*mmPerPixel:NaN;
        const medianWidthMm=Number.isFinite(mmPerPixel)&&mmPerPixel>0?widths.medianWidthPx*mmPerPixel:NaN;
        const maxWidthMm=Number.isFinite(mmPerPixel)&&mmPerPixel>0?widths.maxWidthPx*mmPerPixel:NaN;
        const crackLengthM=Number.isFinite(lengthMm)?lengthMm/1000:NaN;
        const a=Number.isFinite(crackLengthM)?crackLengthM/2:NaN;

        let sigmaGriffith=NaN, sigmaIrwin=NaN;
        if(Number.isFinite(a)&&a>0&&E>0&&gamma>0) sigmaGriffith=Math.sqrt((2*E*gamma)/(Math.PI*a));
        if(Number.isFinite(a)&&a>0&&KIc>0&&Y>0) sigmaIrwin=KIc/(Y*Math.sqrt(Math.PI*a));

        const sigmaGriffith_MPa=Number.isFinite(sigmaGriffith)?sigmaGriffith/1e6:NaN;
        const sigmaIrwin_MPa=Number.isFinite(sigmaIrwin)?sigmaIrwin/1e6:NaN;

        cv.rectangle(result,new cv.Point(bestRect.x,bestRect.y),new cv.Point(bestRect.x+bestRect.width,bestRect.y+bestRect.height),new cv.Scalar(255,0,0,255),2);
        cv.drawContours(result,contours2,bestIndex,new cv.Scalar(0,255,0,255),2);
        const lines=[
          `L = ${Number.isFinite(lengthMm)?lengthMm.toFixed(2)+' mm':crackLengthPx.toFixed(2)+' px'}`,
          `w_max = ${Number.isFinite(maxWidthMm)?maxWidthMm.toFixed(3)+' mm':widths.maxWidthPx.toFixed(2)+' px'}`
        ];
        for(let i=0;i<lines.length;i++){
          cv.putText(result,lines[i],new cv.Point(15,30+i*24),cv.FONT_HERSHEY_SIMPLEX,0.65,new cv.Scalar(255,0,255,255),2);
        }
        cv.imshow('canvasResult',result);

        setReport(
          `Détection automatique terminée.\n\nMesures géométriques :\n- Aire détectée : ${bestArea.toFixed(2)} px²\n- Longueur estimée : ${crackLengthPx.toFixed(2)} px\n- Largeur moyenne : ${widths.meanWidthPx.toFixed(2)} px\n- Largeur médiane : ${widths.medianWidthPx.toFixed(2)} px\n- Largeur maximale : ${widths.maxWidthPx.toFixed(2)} px\n\nConversion en millimètres :\n- Longueur : ${Number.isFinite(lengthMm)?lengthMm.toFixed(2)+' mm':'échelle absente'}\n- Largeur moyenne : ${Number.isFinite(meanWidthMm)?meanWidthMm.toFixed(3)+' mm':'échelle absente'}\n- Largeur médiane : ${Number.isFinite(medianWidthMm)?medianWidthMm.toFixed(3)+' mm':'échelle absente'}\n- Largeur maximale : ${Number.isFinite(maxWidthMm)?maxWidthMm.toFixed(3)+' mm':'échelle absente'}\n\nContrainte critique théorique :\n- Griffith : ${Number.isFinite(sigmaGriffith_MPa)?sigmaGriffith_MPa.toFixed(3)+' MPa':'non calculable'}\n- Irwin : ${Number.isFinite(sigmaIrwin_MPa)?sigmaIrwin_MPa.toFixed(3)+' MPa':'non calculable'}`,
          'ok'
        );

        const graphInterpretation = interpretGraph(sigmaIrwin_MPa, criticalStress);
        setGraphSummary(
          `Lecture automatique du graphe :\n- Point rouge = fissure mesurée\n- Seuil critique = ${criticalStress.toFixed(2)} MPa\n- Valeur Irwin = ${Number.isFinite(sigmaIrwin_MPa) ? sigmaIrwin_MPa.toFixed(3) + ' MPa' : 'non disponible'}\n- Classement = ${graphInterpretation.label}\n\nRègle simple : plus le point rouge est bas dans le graphe, plus la fissure est critique.`,
          graphInterpretation.status
        );

        const diag=diagnosticFissure(maxWidthMm, sigmaIrwin_MPa);
        setDiagnostic(diag.texte, diag.status);
        const crackType = classifyCrackType(bestRect, lengthMm, maxWidthMm);
        setType(crackType.texte, crackType.status);
        if(Number.isFinite(a) && a > 0) drawComparisonChart(a, sigmaGriffith_MPa, sigmaIrwin_MPa, E_GPa, gamma, KIc_MPa, Y, criticalStress);

        src.delete();gray.delete();blur.delete();thresh.delete();morph.delete();cleaned.delete();contours.delete();hierarchy.delete();result.delete();kernel.delete();crackMask.delete();contours2.delete();hierarchy2.delete();if(selectedContour) selectedContour.delete();
      } catch(err){
        console.error(err);
        setReport('Erreur pendant le traitement : '+err,'bad');
        setDiagnostic('Le traitement a échoué.', 'bad');
        setType('Type probable : indéterminé.', 'bad');
        setGraphSummary('Le graphe n’a pas pu être exploité à cause d’une erreur.', 'bad');
      }
    }

    imageInput.addEventListener('change', e => {
      const file = e.target.files[0];
      if(!file) return;
      currentFile = file;
      calibrationPoints = [];
      lastAutoScaleDetection = null;
      stopCalibrationMode();

      const reader = new FileReader();
      reader.onload = evt => {
        hiddenImage.onload = () => {
          sourceImageLoaded = true;
          drawImageFit(hiddenImage, canvasOriginal);
          canvasMask.getContext('2d').clearRect(0,0,canvasMask.width,canvasMask.height);
          canvasResult.getContext('2d').clearRect(0,0,canvasResult.width,canvasResult.height);
          applyAutoParamsFromImage(hiddenImage);
          setDiagnostic('La fissure sera diagnostiquée après détection automatique.', 'warn');
          setType('Le type probable sera estimé après détection automatique.', 'warn');
          setGraphSummary('Le graphe sera exploité après détection de la fissure.', 'warn');
          if(cvReady) setTimeout(() => applyAutoScaleDetection(true), 250);
        };
        hiddenImage.src = evt.target.result;
      };
      reader.readAsDataURL(file);
    });

    autoScaleBtn.addEventListener('click', () => applyAutoScaleDetection(true));
    calibrateBtn.addEventListener('click', () => startCalibrationMode());

    canvasOriginal.addEventListener('click', (e) => {
      if(!calibrationMode || !sourceImageLoaded) return;
      const rectCanvas = canvasOriginal.getBoundingClientRect();
      const mouseX = (e.clientX - rectCanvas.left) * (canvasOriginal.width / rectCanvas.width);
      const mouseY = (e.clientY - rectCanvas.top) * (canvasOriginal.height / rectCanvas.height);
      const rect = getDisplayedImageRect(hiddenImage, canvasOriginal);

      if(mouseX < rect.x || mouseX > rect.x + rect.w || mouseY < rect.y || mouseY > rect.y + rect.h){
        setCalibrationInfo('Clique à l’intérieur de l’image affichée.', 'warn');
        return;
      }

      const imgX = (mouseX - rect.x) / rect.scale;
      const imgY = (mouseY - rect.y) / rect.scale;
      if(calibrationPoints.length < 2) calibrationPoints.push({x:imgX, y:imgY});
      else calibrationPoints = [{x:imgX, y:imgY}];

      redrawOriginalWithCalibration();
      if(calibrationPoints.length === 1) setCalibrationInfo('Premier point enregistré. Clique le deuxième point.', 'warn');
      else if(calibrationPoints.length === 2) finalizeCalibration();
    });

    processBtn.addEventListener('click', detectCrackAndCompute);
    printBtn.addEventListener('click', () => window.print());

    resetBtn.addEventListener('click', () => {
      imageInput.value='';
      sourceImageLoaded=false;
      currentFile=null;
      calibrationMode=false;
      calibrationPoints=[];
      lastAutoScaleDetection=null;
      stopCalibrationMode();
      resetCanvases();
      const cctx=chartCanvas.getContext('2d');
      cctx.clearRect(0,0,chartCanvas.width,chartCanvas.height);
      setReport('Aucune analyse effectuée.');
      setDiagnostic('Le diagnostic apparaîtra ici après traitement.');
      setType('Le type probable de fissure apparaîtra ici après traitement.');
      setGraphSummary('L’interprétation du graphe apparaîtra ici après traitement.', 'warn');
      setCalibrationInfo('Aucune calibration active.', 'warn');
      document.getElementById('mmPerPixel').value='';
      document.getElementById('knownScaleMm').value='10';
      document.getElementById('realDistanceMm').value='10';
      document.getElementById('criticalStress').value='3';
      document.getElementById('blurSize').value='5';
      document.getElementById('blockSize').value='31';
      document.getElementById('cValue').value='8';
      document.getElementById('minArea').value='80';
      document.getElementById('youngE').value='30';
      document.getElementById('gamma').value='1';
      document.getElementById('kic').value='1';
      document.getElementById('geomY').value='1.12';
      document.getElementById('autoScaleZone').value='bottom';
    });

    resetCanvases();
    function waitForOpenCV(){
      if(typeof cv!=='undefined' && cv.getBuildInformation){
        cvReady=true;
        setReport('OpenCV.js chargé. Tu peux importer une photo.', 'ok');
        setDiagnostic('En attente d’une image pour établir le diagnostic.', 'warn');
        setType('En attente d’une image pour estimer le type probable de fissure.', 'warn');
        setGraphSummary('Le graphe sera exploité après traitement.', 'warn');
        setCalibrationInfo('Aucune calibration active.', 'warn');
      } else {
        setTimeout(waitForOpenCV,300);
      }
    }
    waitForOpenCV();
  </script>
</body>
</html>
