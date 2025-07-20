<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Desafío: Estructura de Página Web</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    .draggable { cursor: grab; transition: transform 0.3s ease; }
    .draggable:active { cursor: grabbing; transform: rotate(5deg) scale(1.05); }
    .drop-zone { transition: transform 0.3s ease, background 0.3s ease, border 0.3s ease; border: 2px dashed #cbd5e1; min-height: 60px; }
    .drop-zone.drag-over { border-color: #3b82f6; background-color: #eff6ff; transform: scale(1.02); }
    .drop-zone.filled { border-color: #10b981; background-color: #f0fdf4; }
    .drop-zone.error { border-color: #ef4444; background-color: #fef2f2; animation: shake 0.5s ease-in-out; }
    .correct-placement { animation: success 0.6s ease-in-out; }
    @keyframes success { 0%,100%{transform:scale(1);}50%{transform:scale(1.1);} }
    @keyframes shake { 0%,100%{transform:translateX(0);}25%{transform:translateX(-5px);}75%{transform:translateX(5px);} }
    .timer { font-family: 'Courier New', monospace; font-size: 1.5rem; font-weight: bold; }
  </style>
</head>
<body class="bg-gradient-to-br from-purple-50 to-pink-100 min-h-screen font-sans">
  <div id="start-screen" class="fixed inset-0 bg-gradient-to-br from-purple-600 to-pink-600 flex items-center justify-center z-50">
    <div class="bg-white rounded-xl p-8 text-center shadow-2xl max-w-md mx-4">
      <div class="text-6xl mb-4">🧩</div>
      <h1 class="text-3xl font-bold text-gray-800 mb-4">Desafío Web</h1>
      <p class="text-gray-600 mb-6">¡Descubre dónde va cada parte de una página web! Sin pistas, solo tu conocimiento.</p>
      <input type="text" id="player-name" placeholder="Ingresa tu nombre" class="w-full p-3 border border-gray-300 rounded-lg mb-4 text-center text-lg" maxlength="20">
      <button onclick="startGame()" class="w-full bg-purple-600 hover:bg-purple-700 text-white px-6 py-3 rounded-lg font-medium text-lg mb-2">Comenzar Desafío</button>
      <button onclick="showLeaderboard()" class="w-full bg-gray-600 hover:bg-gray-700 text-white px-6 py-3 rounded-lg font-medium">Ver Clasificación</button>
      <button onclick="showTeacherLogin()" class="w-full mt-3 bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-3 rounded-lg font-medium">👨‍🏫 Acceso Profesor</button>
    </div>
  </div>

  <div class="container mx-auto px-4 py-8">
    <div class="text-center mb-8">
      <h1 class="text-4xl font-bold text-purple-800 mb-4">🎯 Desafío: Estructura Web</h1>
      <div class="bg-white rounded-lg p-4 shadow-md inline-block">
        <div class="flex items-center space-x-6">
          <span class="text-xl font-bold text-purple-600" id="player-display">Jugador: </span>
          <span class="text-xl font-bold text-green-600" id="score">Puntos: 0</span>
          <span class="text-xl font-bold text-blue-600" id="progress">0/5</span>
          <span class="timer text-red-600" id="timer">⏱️ 00:00</span>
        </div>
      </div>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      <!-- Elementos -->
      <div class="bg-white rounded-xl shadow-lg p-4">
        <h2 class="text-2xl font-bold mb-4 text-center">🧩 Elementos a Colocar</h2>
        <div id="elements-container" class="space-y-4">
          <div class="draggable bg-purple-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="header"><span class="text-2xl mr-3">🏠</span>Header</div>
          <div class="draggable bg-blue-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="nav"><span class="text-2xl mr-3">🧭</span>Nav</div>
          <div class="draggable bg-green-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="main"><span class="text-2xl mr-3">📄</span>Main</div>
          <div class="draggable bg-orange-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="sidebar"><span class="text-2xl mr-3">📋</span>Sidebar</div>
          <div class="draggable bg-gray-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="footer"><span class="text-2xl mr-3">🦶</span>Footer</div>
        </div>
      </div>

      <!-- Zonas -->
      <div class="bg-white rounded-xl shadow-lg p-4">
        <h2 class="text-2xl font-bold mb-4 text-center">🎯 Estructura de la Página</h2>
        <div class="space-y-3">
          <div class="drop-zone rounded-lg p-4 flex justify-center items-center text-gray-400 font-medium" data-target="header">Zona 1</div>
          <div class="drop-zone rounded-lg p-4 flex justify-center items-center text-gray-400 font-medium" data-target="nav">Zona 2</div>
          <div class="flex gap-2">
            <div class="drop-zone flex-1 rounded-lg p-4 flex justify-center items-center text-gray-400 font-medium" data-target="main">Zona 3</div>
            <div class="drop-zone w-1/3 rounded-lg p-4 flex justify-center items-center text-gray-400 font-medium" data-target="sidebar">Zona 4</div>
          </div>
          <div class="drop-zone rounded-lg p-4 flex justify-center items-center text-gray-400 font-medium" data-target="footer">Zona 5</div>
        </div>
      </div>
    </div>

    <div id="hint-box" class="mt-8 bg-yellow-50 border-l-4 border-yellow-400 p-4 rounded-lg hidden">
      <div class="flex">
        <span class="text-2xl">💡</span>
        <p class="ml-3 text-yellow-700" id="hint-text"></p>
      </div>
    </div>
  </div>

  <!-- Modales -->
  <div id="leaderboard-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white rounded-xl p-8 shadow-2xl max-w-2xl w-full max-h-96 overflow-y-auto">
      <div class="flex justify-between items-center mb-6">
        <h3 class="text-2xl font-bold text-purple-600">🏆 Clasificación</h3>
        <button onclick="closeLeaderboard()" class="text-gray-500 hover:text-gray-700 text-2xl">×</button>
      </div>
      <div id="leaderboard-content"></div>
      <button onclick="closeLeaderboard()" class="w-full mt-6 bg-purple-600 hover:bg-purple-700 text-white px-6 py-3 rounded-lg">Cerrar</button>
    </div>
  </div>

  <div id="success-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white rounded-xl p-8 text-center shadow-2xl max-w-md w-full">
      <div class="text-6xl mb-4">🎉</div>
      <h3 class="text-2xl font-bold text-green-600 mb-4">¡Desafío Completado!</h3>
      <div id="final-stats" class="text-gray-700 mb-6"></div>
      <button onclick="showLeaderboard()" class="w-full bg-purple-600 hover:bg-purple-700 text-white px-4 py-3 rounded-lg">Ver Clasificación</button>
    </div>
  </div>

  <div id="teacher-login-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white rounded-xl p-8 shadow-2xl max-w-md w-full">
      <div class="text-center mb-6">
        <div class="text-4xl mb-4">👨‍🏫</div>
        <h3 class="text-2xl font-bold text-indigo-600">Acceso Profesor</h3>
      </div>
      <input type="password" id="teacher-password" placeholder="Contraseña" class="w-full p-3 border border-gray-300 rounded-lg text-center mb-4" maxlength="20">
      <div class="flex gap-3">
        <button onclick="closeTeacherLogin()" class="w-1/2 bg-gray-600 text-white px-4 py-3 rounded-lg">Cancelar</button>
        <button onclick="verifyTeacherPassword()" class="w-1/2 bg-indigo-600 text-white px-4 py-3 rounded-lg">Ingresar</button>
      </div>
    </div>
  </div>

  <div id="teacher-panel-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
    <div class="bg-white rounded-xl p-8 shadow-2xl max-w-4xl w-full max-h-96 overflow-y-auto">
      <div class="flex justify-between mb-6">
        <h3 class="text-2xl font-bold text-indigo-600">👨‍🏫 Panel del Profesor</h3>
        <button onclick="closeTeacherPanel()" class="text-gray-500 hover:text-gray-700 text-2xl">×</button>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
        <div class="bg-blue-50 text-center rounded-lg p-4"><div id="total-students" class="text-2xl font-bold text-blue-600">0</div><div>Estudiantes</div></div>
        <div class="bg-green-50 text-center rounded-lg p-4"><div id="avg-score" class="text-2xl font-bold text-green-600">0</div><div>Puntuación</div></div>
        <div class="bg-purple-50 text-center rounded-lg p-4"><div id="avg-time" class="text-2xl font-bold text-purple-600">0:00</div><div>Tiempo</div></div>
      </div>
      <div id="teacher-results-content"></div>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-3 mt-4">
        <button onclick="refreshTeacherPanel()" class="bg-blue-600 text-white px-4 py-3 rounded-lg">🔄 Actualizar</button>
        <button onclick="exportResults()" class="bg-green-600 text-white px-4 py-3 rounded-lg">📊 Exportar</button>
        <button onclick="clearAllResults()" class="bg-red-600 text-white px-4 py-3 rounded-lg">🗑️ Limpiar</button>
        <button onclick="closeTeacherPanel()" class="bg-gray-600 text-white px-4 py-3 rounded-lg">Cerrar</button>
      </div>
    </div>
  </div>

  <script>
    let gameState = { playerName:'', score:0, correctPlacements:0, startTime:null, gameActive:false, draggedElement:null, mistakes:0 };
    const hints = {
      1:"💡 El Header va en la parte superior",
      2:"💡 Nav justo después del header",
      3:"💡 Main ocupa la sección central",
      4:"💡 El Sidebar va a un lado",
      5:"💡 Footer va al final"
    };

    function setupDragAndDrop() {
      document.querySelectorAll('.draggable').forEach(el => {
        el.addEventListener('dragstart', e => { gameState.draggedElement = el; el.style.opacity='0.5'; });
        el.addEventListener('dragend', e => { el.style.opacity='1'; gameState.draggedElement = null; });
      });
      document.querySelectorAll('.drop-zone').forEach(zone => {
        zone.addEventListener('dragover', e => e.preventDefault());
        zone.addEventListener('dragenter', e => { e.preventDefault(); if(!zone.classList.contains('filled')) zone.classList.add('drag-over'); });
        zone.addEventListener('dragleave', e => zone.classList.remove('drag-over'));
        zone.addEventListener('drop', e => {
          e.preventDefault(); zone.classList.remove('drag-over');
          if(gameState.draggedElement && !zone.classList.contains('filled')) processElementPlacement(gameState.draggedElement, zone);
        });
      });
    }

    function processElementPlacement(el, zone) {
      const type = el.dataset.element, target = zone.dataset.target;
      if(type===target) {
        zone.innerHTML = el.outerHTML;
        zone.classList.add('filled','correct-placement'); el.remove();
        gameState.score +=100; gameState.correctPlacements++;
        updateDisplay(); setTimeout(()=> zone.classList.remove('correct-placement'),600);
        if(gameState.correctPlacements===5) setTimeout(completeGame,800);
      } else {
        zone.classList.add('error');
        gameState.mistakes++; gameState.score = Math.max(0, gameState.score-20);
        setTimeout(()=> zone.classList.remove('error'),1000);
        if(gameState.mistakes>=2) showHint();
        updateDisplay();
      }
    }

    function startGame() {
      const name = document.getElementById('player-name').value.trim();
      if(!name) return alert('Por favor ingresa tu nombre');
      gameState.playerName=name; gameState.startTime=Date.now(); gameState.gameActive=true;
      document.getElementById('start-screen').classList.add('hidden');
      document.getElementById('player-display').textContent=`Jugador: ${name}`;
      setupDragAndDrop(); startTimer();
    }

    function startTimer() {
      function tick(){
        if(!gameState.gameActive) return;
        const sec = Math.floor((Date.now()-gameState.startTime)/1000), m=String(Math.floor(sec/60)).padStart(2,'0'), s=String(sec%60).padStart(2,'0');
        document.getElementById('timer').textContent=`⏱️ ${m}:${s}`;
        setTimeout(tick,1000);
      }
      tick();
    }

    function updateDisplay() {
      document.getElementById('score').textContent=`Puntos: ${gameState.score}`;
      document.getElementById('progress').textContent=`${gameState.correctPlacements}/5`;
    }

    function showHint() {
      const nRem = document.querySelectorAll('.draggable').length;
      if(nRem>0){
        document.getElementById('hint-text').textContent = hints[6-nRem] || "💡 ¡Sigue así!";
        document.getElementById('hint-box').classList.remove('hidden');
      }
    }

    function hideHint() {
      document.getElementById('hint-box').classList.add('hidden');
    }

    function completeGame() {
      gameState.gameActive=false;
      const totalSec = Math.floor((Date.now()-gameState.startTime)/1000);
      saveResult(gameState.playerName,gameState.score,totalSec);
      document.getElementById('final-stats').innerHTML = `Puntuación: ${gameState.score} pts<br>Tiempo: ${Math.floor(totalSec/60)}:${String(totalSec%60).padStart(2,'0')}<br>Errores: ${gameState.mistakes}`;
      document.getElementById('success-modal').classList.remove('hidden');
      setTimeout(()=>{ document.getElementById('success-modal').classList.add('hidden'); showLeaderboard(); },3000);
    }

    function saveResult(name,score,time) {
      const key='webStructureResults';
      const arr = JSON.parse(localStorage.getItem(key)||'[]');
      arr.push({name,score,time,date:new Date().toLocaleDateString()});
      arr.sort((a,b)=> b.score-b.score + a.time-b.time );
      localStorage.setItem(key,JSON.stringify(arr));
    }

    function showLeaderboard(){
      const arr=JSON.parse(localStorage.getItem('webStructureResults')||'[]');
      const cont=document.getElementById('leaderboard-content');
      if(arr.length===0){
        cont.innerHTML='<p class="text-center text-gray-500">No hay resultados aún.</p>';
      } else {
        cont.innerHTML = arr.slice(0,10).map((r,i)=>`
          <div class="flex justify-between p-3 bg-gray-50 rounded-lg mb-2">
            <div class="flex items-center"><span class="mr-2">${i<3?['🥇','🥈','🥉'][i]:i+1+'.'}</span><span>${r.name}</span></div>
            <div class="text-right"><div class="font-bold text-purple-600">${r.score} pts</div><div class="text-sm text-gray-500">${Math.floor(r.time/60)}:${String(r.time%60).padStart(2,'0')}</div></div>
          </div>`).join('');
      }
      document.getElementById('leaderboard-modal').classList.remove('hidden');
    }

    function closeLeaderboard(){ document.getElementById('leaderboard-modal').classList.add('hidden'); resetGame(); }

    function showTeacherLogin(){ document.getElementById('teacher-password').value=''; document.getElementById('teacher-login-modal').classList.remove('hidden'); }

    function closeTeacherLogin(){ document.getElementById('teacher-login-modal').classList.add('hidden'); }

    function verifyTeacherPassword(){
      if(document.getElementById('teacher-password').value==='profesor123'){
        closeTeacherLogin();
        showTeacherPanel();
      } else {
        alert('🔒 Contraseña incorrecta');
        document.getElementById('teacher-password').value='';
      }
    }

    function showTeacherPanel(){
      const arr=JSON.parse(localStorage.getItem('webStructureResults')||'[]');
      document.getElementById('total-students').textContent=arr.length;
      document.getElementById('avg-score').textContent = arr.length ? Math.round(arr.reduce((s,r)=>s+r.score,0)/arr.length) : 0;
      const avgSec = arr.length ? Math.round(arr.reduce((s,r)=>s+r.time,0)/arr.length) : 0;
      document.getElementById('avg-time').textContent = `${Math.floor(avgSec/60)}:${String(avgSec%60).padStart(2,'0')}`;
      document.getElementById('teacher-results-content').innerHTML = arr.map((r,i)=>`
        <div class="flex justify-between p-3 bg-gray-50 rounded-lg mb-2">
          <div><span>${i<3?['🥇','🥈','🥉'][i]:i+1+'.'} ${r.name}</span></div>
          <div class="text-right"><span>${r.score} pts</span><br><span>${Math.floor(r.time/60)}:${String(r.time%60).padStart(2,'0')}</span><br><span>${r.date}</span></div>
        </div>`).join('');
      document.getElementById('teacher-panel-modal').classList.remove('hidden');
    }

    function closeTeacherPanel(){ document.getElementById('teacher-panel-modal').classList.add('hidden'); }

    function refreshTeacherPanel(){ showTeacherPanel(); alert('🔄 Panel actualizado'); }

    function clearAllResults(){
      const arr=JSON.parse(localStorage.getItem('webStructureResults')||'[]'), tot=arr.length;
      if(!tot)return alert('ℹ️ No hay resultados para eliminar');
      if(confirm(`¿Eliminar ${tot} resultados? Esta acción es irreversible.`)){
        localStorage.removeItem('webStructureResults');
        showTeacherPanel();
        alert('✅ Resultados eliminados');
      }
    }

    function exportResults(){
      const arr=JSON.parse(localStorage.getItem('webStructureResults')||'[]');
      if(!arr.length) return alert('ℹ️ No hay resultados para exportar');
      let csv='Pos,Nombre,Puntos,Tiempo,Fecha\n';
      arr.forEach((r,i)=> csv+=`${i+1},"${r.name}",${r.score},"${Math.floor(r.time/60)}:${String(r.time%60).padStart(2,'0')}","${r.date}"\n`);
      const blob=new Blob([csv],{type:'text/csv'}), a=document.createElement('a');
      a.href=URL.createObjectURL(blob); a.download=`resultados_${new Date().toISOString().split('T')[0]}.csv`;
      a.click(); alert('📊 Exportado correctamente');
    }

    function resetGame(){
      gameState={playerName:'', score:0, correctPlacements:0, startTime:null, gameActive:false, draggedElement:null, mistakes:0};
      document.getElementById('start-screen').classList.remove('hidden');
      document.querySelectorAll('.drop-zone').forEach((z,i)=>{
        z.className='drop-zone rounded-lg p-4 flex justify-center items-center text-gray-400 font-medium';
        z.textContent=`Zona ${i+1}`;
      });
      document.getElementById('elements-container').innerHTML=`
        <div class="draggable bg-purple-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="header">🏠 Header</div>
        <div class="draggable bg-blue-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="nav">🧭 Nav</div>
        <div class="draggable bg-green-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="main">📄 Main</div>
        <div class="draggable bg-orange-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="sidebar">📋 Sidebar</div>
        <div class="draggable bg-gray-500 text-white p-4 rounded-lg shadow-md" draggable="true" data-element="footer">🦶 Footer</div>`;
      updateDisplay(); hideHint(); setupDragAndDrop();
    }
  </script>
</body>
</html>
