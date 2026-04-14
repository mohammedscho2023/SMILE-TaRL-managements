<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>TaRL Complete M&E | Woreda Data Entry · Gender Disaggregated</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { background: #eef5f0; font-family: 'Inter', sans-serif; color: #1a3a2e; padding: 16px; }
        .app-container { max-width: 1600px; margin: 0 auto; }
        .main-header { background: linear-gradient(115deg, #0b3326 0%, #1b5e45 100%); border-radius: 20px; padding: 18px 22px; margin-bottom: 20px; color: white; }
        .brand h1 { font-size: 0.95rem; font-weight: 700; display: flex; align-items: center; gap: 8px; flex-wrap: wrap; }
        .brand i { background: #ffcd6b; color: #1a4d34; border-radius: 50px; padding: 8px; }
        .sub { color: #c7f0e2; margin-top: 4px; font-size: 0.55rem; }
        .nav-pills { display: flex; flex-wrap: wrap; gap: 4px; margin-top: 12px; border-bottom: 1px solid rgba(255,255,255,0.2); padding-bottom: 6px; }
        .nav-btn { background: transparent; border: none; font-weight: 600; padding: 4px 10px; border-radius: 40px; font-size: 0.65rem; cursor: pointer; color: #f0faf5; transition: 0.2s; }
        .nav-btn i { margin-right: 4px; }
        .nav-btn.active { background: #ffcd6b; color: #1b422f; }
        .panel { display: none; animation: fadeIn 0.25s ease; }
        .panel.active-panel { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(6px);} to { opacity: 1; transform: translateY(0);} }
        .card { background: white; border-radius: 20px; padding: 20px; margin-bottom: 20px; box-shadow: 0 4px 12px rgba(0,0,0,0.04); overflow-x: auto; }
        .form-row { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 12px; margin-bottom: 16px; align-items: flex-end; }
        .input-group { display: flex; flex-direction: column; gap: 4px; }
        .input-group label { font-weight: 700; font-size: 0.6rem; text-transform: uppercase; color: #548b74; }
        input, select { padding: 8px 10px; border-radius: 12px; border: 1.5px solid #e0ede5; font-size: 0.7rem; background: white; }
        button { background: #1e5e48; border: none; padding: 8px 16px; border-radius: 30px; font-weight: 600; color: white; cursor: pointer; font-size: 0.7rem; transition: 0.2s; }
        button i { margin-right: 5px; }
        button.btn-outline { background: white; border: 1.5px solid #caddd4; color: #1e5e48; }
        button:hover { background: #0f4635; transform: translateY(-1px); }
        .stats-grid { display: flex; flex-wrap: wrap; gap: 12px; margin-bottom: 20px; }
        .stat-card { background: white; flex: 1; min-width: 130px; border-radius: 16px; padding: 12px; border-left: 4px solid #ffcd6b; }
        .stat-number { font-size: 1.3rem; font-weight: 800; color: #1e5e48; }
        .progress-bar { background: #e3f0ea; border-radius: 20px; height: 6px; width: 100%; overflow: hidden; margin-top: 4px; }
        .progress-fill { background: #ffcd6b; width: 0%; height: 100%; }
        .badge { display: inline-block; padding: 3px 10px; border-radius: 20px; font-size: 0.6rem; font-weight: 600; }
        .badge-success { background: #d4f0e3; color: #1a6e4a; }
        .badge-warning { background: #fff1db; color: #b55f00; }
        .badge-info { background: #eafaf2; color: #1e5e48; }
        .edit-input { width: 80px; padding: 4px; border-radius: 8px; border: 1px solid #caddd4; text-align: center; }
        .unit-badge { background: #e8f3ef; padding: 2px 8px; border-radius: 20px; font-size: 0.6rem; color: #1e5e48; }
        .gender-row { display: flex; gap: 15px; align-items: center; background: #f9fefb; padding: 8px; border-radius: 12px; margin-top: 5px; }
        .gender-field { display: flex; flex-direction: column; gap: 3px; }
        .gender-field label { font-size: 0.6rem; font-weight: bold; }
        .woreda-card { background: #fefef7; border-radius: 16px; padding: 15px; margin-bottom: 15px; border-left: 4px solid #ffcd6b; }
        @media (max-width: 768px) { .form-row { grid-template-columns: 1fr; } .edit-input { width: 60px; } }
    </style>
</head>
<body>
<div class="app-container">
    <div class="main-header">
        <div class="brand"><h1><i class="fas fa-chalkboard-user"></i> TaRL M&E System <span style="font-size:0.55rem;">Woreda Data Entry · Gender Disaggregated (Boys/Men · Girls/Women)</span></h1>
        <div class="sub">Training Activities: Track Male/Female Participants | Non-Training: Track Quantity | 5 Woredas: Babile, Chinaksan, Mi'o, Yabelo, Taltale</div></div>
        <div class="nav-pills">
            <button class="nav-btn active" data-panel="woredaEntryPanel"><i class="fas fa-edit"></i> Woreda Data Entry</button>
            <button class="nav-btn" data-panel="summaryPanel"><i class="fas fa-chart-line"></i> Summary Dashboard</button>
            <button class="nav-btn" data-panel="reportPanel"><i class="fas fa-file-alt"></i> Reports</button>
        </div>
    </div>

    <!-- WOREDA DATA ENTRY PANEL -->
    <div id="woredaEntryPanel" class="panel active-panel">
        <div class="card">
            <h2><i class="fas fa-edit"></i> Woreda-Level Activity Data Entry</h2>
            <div class="form-row">
                <div class="input-group"><label>Select Woreda</label><select id="entryWoreda"><option value="Babile">Babile</option><option value="Chinaksan">Chinaksan</option><option value="Mi'o">Mi'o</option><option value="Yabelo">Yabelo</option><option value="Taltale">Taltale</option></select></div>
                <div class="input-group"><label>Select Activity</label><select id="entryActivity"></select></div>
            </div>
            <div id="genderFieldsContainer" style="margin-top: 15px; margin-bottom: 20px;"></div>
            <div style="display: flex; gap: 12px; justify-content: flex-end;">
                <button id="saveWoredaDataBtn"><i class="fas fa-save"></i> Save Record</button>
                <button id="resetWoredaBtn" class="btn-outline"><i class="fas fa-trash"></i> Reset All Woreda Data</button>
            </div>
        </div>

        <div class="card">
            <h2><i class="fas fa-table"></i> Woreda Activity Data Summary</h2>
            <div style="overflow-x:auto;">
                <table id="woredaDataTable">
                    <thead><tr><th>Woreda</th><th>Activity Code</th><th>Activity</th><th>Type</th><th>Male/Boy</th><th>Female/Girl</th><th>Total</th><th>Date</th><th>Action</th></tr></thead>
                    <tbody id="woredaDataBody"></tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- SUMMARY DASHBOARD PANEL -->
    <div id="summaryPanel" class="panel">
        <div class="stats-grid" id="summaryStats"></div>
        <div class="card">
            <h2><i class="fas fa-chart-pie"></i> Woreda Performance</h2>
            <canvas id="woredaChart" height="200" style="max-width:100%;"></canvas>
        </div>
        <div class="card">
            <h2><i class="fas fa-chart-bar"></i> Training Activities - Gender Distribution</h2>
            <canvas id="genderChart" height="200" style="max-width:100%;"></canvas>
        </div>
    </div>

    <!-- REPORT PANEL -->
    <div id="reportPanel" class="panel">
        <div class="card">
            <h2><i class="fas fa-file-alt"></i> Comprehensive Woreda Report</h2>
            <div id="reportContent"></div>
            <button id="exportReportBtn" class="btn-outline" style="margin-top:16px;"><i class="fas fa-download"></i> Export CSV</button>
            <button id="printReportBtn" class="btn-outline"><i class="fas fa-print"></i> Print Report</button>
        </div>
    </div>
</div>

<script>
    // Activity List with Types
    const activities = [
        { code: "4.1.6", name: "Print TaRL teachers guideline & assessment tools", type: "Non-Training", unit: "Manuals" },
        { code: "4.2.6", name: "Print supplementary reading materials (SRMs)", type: "Non-Training", unit: "SRMs" },
        { code: "4.2.7", name: "Procure SRMs book bank boxes/shelves", type: "Non-Training", unit: "Schools" },
        { code: "4.3", name: "Intra/inter-school reading & numeracy competitions", type: "Non-Training", unit: "Schools" },
        { code: "4.4.2", name: "Make classrooms & latrines accessible for CWDs", type: "Non-Training", unit: "Schools" },
        { code: "4.4.3", name: "Procure & distribute assistive devices for CWDs", type: "Non-Training", unit: "CWDs" },
        { code: "4.5", name: "Strengthen & establish reading clubs", type: "Non-Training", unit: "Schools" },
        { code: "4.5.1", name: "Training of Trainers (ToT) for master trainers", type: "Training", unit: "Master Trainers" },
        { code: "4.5.2", name: "Train teachers on TaRL & core reading skills", type: "Training", unit: "Teachers" },
        { code: "4.5.3", name: "Train model teachers & cluster supervisors as mentors", type: "Training", unit: "Mentors" },
        { code: "4.5.4", name: "Train school administrators & WEO experts", type: "Training", unit: "Personnel" },
        { code: "4.5.5", name: "Performance-based incentives", type: "Non-Training", unit: "Honorees" },
        { code: "4.5.6", name: "Conduct literacy skills assessment", type: "Training", unit: "Teachers" },
        { code: "4.6.1", name: "Multi-sectoral WASH training", type: "Training", unit: "Participants" },
        { code: "4.6.2a", name: "Media broadcast for SBCC", type: "Non-Training", unit: "Minutes" },
        { code: "4.6.2b", name: "Print banners, flyers, posters", type: "Non-Training", unit: "Schools" },
        { code: "4.6.2c", name: "Support mini-media clubs", type: "Non-Training", unit: "Schools" },
        { code: "4.8.1", name: "Orient gender club leaders", type: "Training", unit: "Participants" },
        { code: "4.8.2", name: "Train PTA, KETB, religious leaders", type: "Training", unit: "Participants" }
    ];

    const woredas = ["Babile", "Chinaksan", "Mi'o", "Yabelo", "Taltale"];
    
    // Data structure: woredaData[woreda][activityCode] = { male, female, total, date }
    let woredaData = {};

    function initData() {
        for (let w of woredas) {
            woredaData[w] = {};
            for (let act of activities) {
                woredaData[w][act.code] = { male: 0, female: 0, total: 0, date: "" };
            }
        }
    }

    function loadData() {
        const stored = localStorage.getItem("tarl_woreda_gender_data");
        if (stored) {
            woredaData = JSON.parse(stored);
        } else {
            initData();
        }
        renderAll();
    }

    function saveData() {
        localStorage.setItem("tarl_woreda_gender_data", JSON.stringify(woredaData));
        renderAll();
    }

    function populateActivitySelect() {
        const select = document.getElementById("entryActivity");
        if (!select) return;
        select.innerHTML = '<option value="">-- Select Activity --</option>';
        for (let act of activities) {
            select.innerHTML += `<option value="${act.code}" data-type="${act.type}" data-unit="${act.unit}">${act.code} - ${act.name.substring(0, 50)} (${act.type})</option>`;
        }
        select.onchange = function() {
            const selectedCode = this.value;
            const activity = activities.find(a => a.code === selectedCode);
            const container = document.getElementById("genderFieldsContainer");
            if (!container) return;
            if (activity && activity.type === "Training") {
                container.innerHTML = `
                    <div class="gender-row">
                        <div class="gender-field"><label><i class="fas fa-mars"></i> Boys/Men</label><input type="number" id="inputMale" value="0" min="0" style="width:120px;"></div>
                        <div class="gender-field"><label><i class="fas fa-venus"></i> Girls/Women</label><input type="number" id="inputFemale" value="0" min="0" style="width:120px;"></div>
                        <div class="gender-field"><label><i class="fas fa-users"></i> Total</label><input type="text" id="inputTotal" readonly style="background:#f0f7f3; width:100px;"></div>
                    </div>
                `;
                const maleInput = document.getElementById("inputMale");
                const femaleInput = document.getElementById("inputFemale");
                const totalInput = document.getElementById("inputTotal");
                const updateTotal = () => { totalInput.value = (parseInt(maleInput.value) || 0) + (parseInt(femaleInput.value) || 0); };
                maleInput.oninput = updateTotal;
                femaleInput.oninput = updateTotal;
            } else if (activity && activity.type === "Non-Training") {
                container.innerHTML = `
                    <div class="gender-row">
                        <div class="gender-field"><label><i class="fas fa-box"></i> Quantity (${activity.unit})</label><input type="number" id="inputQuantity" value="0" min="0" style="width:150px;"></div>
                    </div>
                `;
            } else {
                container.innerHTML = "<p>Select an activity first</p>";
            }
        };
    }

    function saveWoredaRecord() {
        const woreda = document.getElementById("entryWoreda").value;
        const activityCode = document.getElementById("entryActivity").value;
        if (!activityCode) { alert("Please select an activity"); return; }
        const activity = activities.find(a => a.code === activityCode);
        if (!activity) return;
        
        if (activity.type === "Training") {
            const male = parseInt(document.getElementById("inputMale")?.value) || 0;
            const female = parseInt(document.getElementById("inputFemale")?.value) || 0;
            const total = male + female;
            if (total === 0 && male === 0 && female === 0) {
                if (!confirm("Save zero values? This will clear existing data.")) return;
            }
            woredaData[woreda][activityCode] = { male, female, total, date: new Date().toLocaleDateString() };
        } else {
            const quantity = parseInt(document.getElementById("inputQuantity")?.value) || 0;
            woredaData[woreda][activityCode] = { male: quantity, female: 0, total: quantity, date: new Date().toLocaleDateString() };
        }
        saveData();
        alert(`Data saved for ${woreda} - ${activityCode}`);
        document.getElementById("entryActivity").value = "";
        document.getElementById("genderFieldsContainer").innerHTML = "<p>Select an activity to enter data</p>";
    }

    function deleteRecord(woreda, code) {
        if (confirm(`Delete record for ${woreda} - ${code}?`)) {
            woredaData[woreda][code] = { male: 0, female: 0, total: 0, date: "" };
            saveData();
        }
    }

    function resetAllData() {
        if (confirm("WARNING: This will reset ALL woreda data to zero. Are you sure?")) {
            initData();
            saveData();
        }
    }

    function renderWoredaDataTable() {
        const tbody = document.getElementById("woredaDataBody");
        if (!tbody) return;
        tbody.innerHTML = "";
        for (let w of woredas) {
            for (let act of activities) {
                const data = woredaData[w][act.code];
                if (data && (data.male > 0 || data.female > 0 || data.total > 0)) {
                    const row = tbody.insertRow();
                    row.insertCell(0).innerHTML = w;
                    row.insertCell(1).innerHTML = act.code;
                    row.insertCell(2).innerHTML = act.name.substring(0, 40);
                    row.insertCell(3).innerHTML = `<span class="badge" style="background:${act.type==='Training'?'#e8f3ef':'#fff1db'}">${act.type}</span>`;
                    row.insertCell(4).innerHTML = act.type === "Training" ? data.male : "-";
                    row.insertCell(5).innerHTML = act.type === "Training" ? data.female : "-";
                    row.insertCell(6).innerHTML = data.total;
                    row.insertCell(7).innerHTML = data.date || "-";
                    const delCell = row.insertCell(8);
                    const delBtn = document.createElement("button");
                    delBtn.innerHTML = '<i class="fas fa-trash"></i>';
                    delBtn.style.background = "#c23b22";
                    delBtn.style.padding = "3px 8px";
                    delBtn.onclick = () => deleteRecord(w, act.code);
                    delCell.appendChild(delBtn);
                }
            }
        }
        if (tbody.children.length === 0) {
            tbody.innerHTML = '<tr><td colspan="9" style="text-align:center;">No data entered yet. Use the form above.</td></tr>';
        }
    }

    function renderDashboard() {
        let totalMale = 0, totalFemale = 0, totalNonTraining = 0;
        for (let w of woredas) {
            for (let act of activities) {
                const data = woredaData[w][act.code];
                if (act.type === "Training") {
                    totalMale += data.male;
                    totalFemale += data.female;
                } else {
                    totalNonTraining += data.total;
                }
            }
        }
        const woredaTotals = woredas.map(w => {
            let sum = 0;
            for (let act of activities) sum += woredaData[w][act.code].total;
            return sum;
        });
        const overallTotal = totalMale + totalFemale + totalNonTraining;
        
        document.getElementById("summaryStats").innerHTML = `
            <div class="stat-card"><strong>👨 Total Male/Boy</strong><div class="stat-number">${totalMale.toLocaleString()}</div></div>
            <div class="stat-card"><strong>👩 Total Female/Girl</strong><div class="stat-number">${totalFemale.toLocaleString()}</div></div>
            <div class="stat-card"><strong>📦 Non-Training Total</strong><div class="stat-number">${totalNonTraining.toLocaleString()}</div></div>
            <div class="stat-card"><strong>📊 Overall Total</strong><div class="stat-number">${overallTotal.toLocaleString()}</div></div>
        `;
        
        const ctx = document.getElementById('woredaChart')?.getContext('2d');
        if (ctx) {
            if (window.woredaChart) window.woredaChart.destroy();
            window.woredaChart = new Chart(ctx, { type: 'bar', data: { labels: woredas, datasets: [{ label: 'Total Achieved', data: woredaTotals, backgroundColor: '#1e5e48' }] }, options: { responsive: true } });
        }
        
        const ctx2 = document.getElementById('genderChart')?.getContext('2d');
        if (ctx2) {
            if (window.genderChart) window.genderChart.destroy();
            window.genderChart = new Chart(ctx2, { type: 'pie', data: { labels: ['Male/Boy Participants', 'Female/Girl Participants'], datasets: [{ data: [totalMale, totalFemale], backgroundColor: ['#1e5e48', '#ffcd6b'] }] } });
        }
    }

    function renderReport() {
        let totalMale = 0, totalFemale = 0, totalNonTraining = 0;
        let trainingActivitiesDetail = "";
        let nonTrainingDetail = "";
        
        for (let w of woredas) {
            for (let act of activities) {
                const data = woredaData[w][act.code];
                if (act.type === "Training") {
                    totalMale += data.male;
                    totalFemale += data.female;
                    if (data.male > 0 || data.female > 0) {
                        trainingActivitiesDetail += `<tr><td>${w}</td><td>${act.code}</td><td>${act.name.substring(0, 40)}</td><td>${data.male}</td><td>${data.female}</td><td>${data.total}</td></tr>`;
                    }
                } else {
                    totalNonTraining += data.total;
                    if (data.total > 0) {
                        nonTrainingDetail += `<tr><td>${w}</td><td>${act.code}</td><td>${act.name.substring(0, 40)}</td><td>${data.total}</td><td>${act.unit}</td></tr>`;
                    }
                }
            }
        }
        
        document.getElementById("reportContent").innerHTML = `
            <h3>Oromia TaRL Woreda Report</h3>
            <p><strong>Report Date:</strong> ${new Date().toLocaleDateString()}</p>
            <h4>Training Activities - Gender Disaggregated</h4>
            <table style="width:100%; border-collapse:collapse;"><thead><tr><th>Woreda</th><th>Code</th><th>Activity</th><th>Male/Boy</th><th>Female/Girl</th><th>Total</th></tr></thead><tbody>${trainingActivitiesDetail || '<tr><td colspan="6">No training data</td></tr>'}</tbody></table>>
            <h4 style="margin-top:20px;">Non-Training Activities</h4>
            <table style="width:100%; border-collapse:collapse;"><thead><tr><th>Woreda</th><th>Code</th><th>Activity</th><th>Quantity</th><th>Unit</th></tr></thead><tbody>${nonTrainingDetail || '<tr><td colspan="5">No non-training data</td></tr>'}</tbody></table>>
            <p style="margin-top:20px;"><strong>Summary:</strong> Total Male/Boy Participants: ${totalMale} | Total Female/Girl Participants: ${totalFemale} | Total Non-Training Units: ${totalNonTraining}</p>
        `;
    }

    function exportCSV() {
        let csv = "Woreda,Activity Code,Activity Name,Type,Male/Boy,Female/Girl,Total,Unit,Date\n";
        for (let w of woredas) {
            for (let act of activities) {
                const data = woredaData[w][act.code];
                if (data && (data.male > 0 || data.female > 0 || data.total > 0)) {
                    csv += `"${w}","${act.code}","${act.name.replace(/"/g, '""')}","${act.type}",${act.type==="Training"?data.male:"-"},${act.type==="Training"?data.female:"-"},${data.total},"${act.unit}","${data.date || ""}"\n`;
                }
            }
        }
        const blob = new Blob([csv], { type: "text/csv" });
        const link = document.createElement("a");
        link.href = URL.createObjectURL(blob);
        link.download = "tarl_woreda_gender_report.csv";
        link.click();
        URL.revokeObjectURL(link.href);
    }

    function printReport() { window.print(); }

    function renderAll() {
        renderWoredaDataTable();
        renderDashboard();
        renderReport();
    }

    // Event Listeners
    document.getElementById("saveWoredaDataBtn")?.addEventListener("click", saveWoredaRecord);
    document.getElementById("resetWoredaBtn")?.addEventListener("click", resetAllData);
    document.getElementById("exportReportBtn")?.addEventListener("click", exportCSV);
    document.getElementById("printReportBtn")?.addEventListener("click", printReport);
    
    document.querySelectorAll('.nav-btn').forEach(btn => {
        btn.addEventListener('click', function() {
            const panelId = this.getAttribute('data-panel');
            document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
            this.classList.add('active');
            document.querySelectorAll('.panel').forEach(p => p.classList.remove('active-panel'));
            document.getElementById(panelId).classList.add('active-panel');
            if (panelId === 'summaryPanel') renderDashboard();
            if (panelId === 'woredaEntryPanel') renderWoredaDataTable();
            if (panelId === 'reportPanel') renderReport();
        });
    });
    
    populateActivitySelect();
    loadData();
</script>
</body>
</html>
<!DOCTYPE html>
<html lang="om">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>TaRL Complete M&E | Student Assessment (Baseline/Midline/Endline) · Zonal Summary · Activities Plan</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;500;600;700;800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { background: #eef5f0; font-family: 'Inter', sans-serif; color: #1a3a2e; padding: 16px; }
        .app-container { max-width: 1600px; margin: 0 auto; }
        .main-header { background: linear-gradient(115deg, #0b3326 0%, #1b5e45 100%); border-radius: 20px; padding: 18px 22px; margin-bottom: 20px; color: white; }
        .brand h1 { font-size: 0.95rem; font-weight: 700; display: flex; align-items: center; gap: 8px; flex-wrap: wrap; }
        .brand i { background: #ffcd6b; color: #1a4d34; border-radius: 50px; padding: 8px; }
        .sub { color: #c7f0e2; margin-top: 4px; font-size: 0.55rem; }
        .nav-pills { display: flex; flex-wrap: wrap; gap: 4px; margin-top: 12px; border-bottom: 1px solid rgba(255,255,255,0.2); padding-bottom: 6px; }
        .nav-btn { background: transparent; border: none; font-weight: 600; padding: 4px 10px; border-radius: 40px; font-size: 0.65rem; cursor: pointer; color: #f0faf5; transition: 0.2s; }
        .nav-btn i { margin-right: 4px; }
        .nav-btn.active { background: #ffcd6b; color: #1b422f; }
        .panel { display: none; animation: fadeIn 0.25s ease; }
        .panel.active-panel { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(6px);} to { opacity: 1; transform: translateY(0);} }
        .card { background: white; border-radius: 20px; padding: 20px; margin-bottom: 20px; box-shadow: 0 4px 12px rgba(0,0,0,0.04); overflow-x: auto; }
        .form-row { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 12px; margin-bottom: 16px; align-items: flex-end; }
        .input-group { display: flex; flex-direction: column; gap: 4px; }
        .input-group label { font-weight: 700; font-size: 0.6rem; text-transform: uppercase; color: #548b74; }
        input, select { padding: 8px 10px; border-radius: 12px; border: 1.5px solid #e0ede5; font-size: 0.7rem; background: white; }
        button { background: #1e5e48; border: none; padding: 8px 16px; border-radius: 30px; font-weight: 600; color: white; cursor: pointer; font-size: 0.7rem; transition: 0.2s; }
        button i { margin-right: 5px; }
        button.btn-outline { background: white; border: 1.5px solid #caddd4; color: #1e5e48; }
        button:hover { background: #0f4635; transform: translateY(-1px); }
        .stats-grid { display: flex; flex-wrap: wrap; gap: 12px; margin-bottom: 20px; }
        .stat-card { background: white; flex: 1; min-width: 130px; border-radius: 16px; padding: 12px; border-left: 4px solid #ffcd6b; }
        .stat-number { font-size: 1.3rem; font-weight: 800; color: #1e5e48; }
        .progress-bar { background: #e3f0ea; border-radius: 20px; height: 6px; width: 100%; overflow: hidden; margin-top: 4px; }
        .progress-fill { background: #ffcd6b; width: 0%; height: 100%; }
        .badge { display: inline-block; padding: 3px 10px; border-radius: 20px; font-size: 0.6rem; font-weight: 600; }
        .badge-success { background: #d4f0e3; color: #1a6e4a; }
        .badge-warning { background: #fff1db; color: #b55f00; }
        .badge-info { background: #eafaf2; color: #1e5e48; }
        .edit-input { width: 80px; padding: 4px; border-radius: 8px; border: 1px solid #caddd4; text-align: center; }
        .unit-badge { background: #e8f3ef; padding: 2px 8px; border-radius: 20px; font-size: 0.6rem; color: #1e5e48; }
        .binary-group { display: flex; gap: 8px; flex-wrap: wrap; margin: 8px 0; }
        .binary-option { display: flex; align-items: center; gap: 4px; background: #f9fefb; padding: 3px 8px; border-radius: 20px; font-size: 0.65rem; cursor: pointer; }
        .binary-option input { width: 14px; height: 14px; cursor: pointer; }
        .level-section { background: #f9fefb; border-radius: 12px; padding: 10px; margin-bottom: 10px; border: 1px solid #e0ede5; }
        .level-title { font-weight: 800; font-size: 0.7rem; color: #1e5e48; margin-bottom: 6px; }
        .phase-selector { display: flex; gap: 10px; margin-bottom: 16px; background: #f0f7f3; padding: 10px; border-radius: 16px; flex-wrap: wrap; }
        .phase-btn { background: #caddd4; color: #1a3a2e; padding: 4px 16px; border-radius: 30px; cursor: pointer; font-size: 0.65rem; font-weight: bold; border: none; }
        .phase-btn.active-phase { background: #1e5e48; color: white; }
        @media (max-width: 768px) { .form-row { grid-template-columns: 1fr; } .edit-input { width: 60px; } }
    </style>
</head>
<body>
<div class="app-container">
    <div class="main-header">
        <div class="brand"><h1><i class="fas fa-chalkboard-user"></i> TaRL Complete M&E System <span style="font-size:0.55rem;">Baseline · Midline · Endline · Zonal Summary</span></h1>
        <div class="sub">Afaan Oromoo: Jalqabdoota → Qubee → Jecha → Keeyyata Salphaa → Seeneessaa | English: Beginner → Letter → Word → Paragraph → Story | Herrega: Levels 0-4</div></div>
        <div class="nav-pills">
            <button class="nav-btn active" data-panel="studentPanel"><i class="fas fa-child"></i> Student Assessment</button>
            <button class="nav-btn" data-panel="activitiesPanel"><i class="fas fa-calendar-alt"></i> Activities Plan</button>
            <button class="nav-btn" data-panel="zonalPanel"><i class="fas fa-globe"></i> Zonal Summary</button>
            <button class="nav-btn" data-panel="dashboardPanel"><i class="fas fa-chart-line"></i> Dashboard</button>
            <button class="nav-btn" data-panel="reportPanel"><i class="fas fa-file-alt"></i> Reports</button>
        </div>
    </div>

    <!-- STUDENT ASSESSMENT PANEL with Baseline/Midline/Endline Phases -->
    <div id="studentPanel" class="panel active-panel">
        <div class="card">
            <div class="phase-selector">
                <button class="phase-btn active-phase" data-phase="baseline">📋 Baseline (Y1 Start)</button>
                <button class="phase-btn" data-phase="midline">📊 Midline (Y2)</button>
                <button class="phase-btn" data-phase="endline">🏆 Endline (Y3)</button>
            </div>
            <h2><i class="fas fa-user-plus"></i> Student Registration (Profile auto-feed, Assessment per Phase)</h2>
            <div class="form-row">
                <div class="input-group"><label>Zone / Godina</label><input type="text" id="regZone" placeholder="Guji"></div>
                <div class="input-group"><label>Woreda / Aanaa</label><input type="text" id="regWoreda" placeholder="Guji Aanaa"></div>
                <div class="input-group"><label>School ID</label><input type="text" id="regSchoolId" placeholder="SCH001"></div>
                <div class="input-group"><label>School Name</label><input type="text" id="regSchoolName" placeholder="School Name"></div>
                <div class="input-group"><label>Learner Full Name</label><input type="text" id="regFullName" placeholder="Almaz Tadese"></div>
                <div class="input-group"><label>Grade / Kutaa</label><select id="regGrade"><option value="3">Kutaa 3</option><option value="4">Kutaa 4</option><option value="5">Kutaa 5</option><option value="6">Kutaa 6</option></select></div>
                <div class="input-group"><label>Gender</label><select id="regGender"><option value="Dhi">Dhiirraa</option><option value="Dub">Dubartii</option></select></div>
                <div class="input-group"><label>Special Need</label><select id="regSpecial"><option value="0">0=Iddoo</option><option value="1">1=Arguu</option><option value="2">2=Dhaga'uu</option><option value="3">3=Qaamaa</option><option value="4">4=Waliifgaluu</option><option value="5">5=Sammu</option><option value="6">6=Amalaa</option></select></div>
            </div>
            <div class="level-section"><div class="level-title">📐 Herrega (Numeracy) Levels 0-4</div><div class="binary-group" id="mathGroup"></div></div>
            <div class="level-section"><div class="level-title">📖 Afaan Oromoo (Jalqabdoota→Qubee→Jecha→Keey.Salphaa→Seeneessaa)</div><div class="binary-group" id="oromoGroup"></div></div>
            <div class="level-section"><div class="level-title">🇬🇧 English (Beginner→Letter→Word→Paragraph→Story)</div><div class="binary-group" id="engGroup"></div></div>
            <div style="display: flex; gap: 12px; justify-content: flex-end; margin-top: 20px;"><button id="addStudentBtn"><i class="fas fa-save"></i> Register for Selected Phase</button><button id="clearStudentBtn" class="btn-outline">Clear Form</button></div>
        </div>
        <div class="card"><h2><i class="fas fa-table"></i> Registered Students (Profile + All Phases)</h2><div style="overflow-x:auto;"><table id="studentTable"><thead><tr><th>Name</th><th>School</th><th>Grade</th><th>Gender</th><th>Baseline Oromo</th><th>Midline Oromo</th><th>Endline Oromo</th><th>Action</th></tr></thead><tbody id="studentBody"></tbody></table></div><button id="exportStudentBtn" class="btn-outline" style="margin-top:12px;"><i class="fas fa-download"></i> Export Student Data CSV</button></div>
    </div>

    <!-- ACTIVITIES PLAN PANEL with Unit of Measurements and Target Plan -->
    <div id="activitiesPanel" class="panel">
        <div class="card">
            <h2><i class="fas fa-list-check"></i> Oromia Region Activities Plan (Y2 2026) - with Unit of Measurements & Target Plan</h2>
            <p style="font-size:0.7rem; margin-bottom:15px;"><span class="unit-badge"><i class="fas fa-users"></i> Training: People/Participants/Trainees</span> <span class="unit-badge"><i class="fas fa-box"></i> Non-Training: Materials/Schools/Units</span></p>
            <div style="overflow-x:auto;"><table id="activitiesTable"><thead><tr><th>Code</th><th>Activity</th><th>Type</th><th>Unit</th><th>Target Plan</th><th>Achieved</th><th>Progress</th><th>Status</th><th>Action</th></tr></thead><tbody id="activitiesBody"></tbody></table></div>
            <div style="margin-top: 20px;"><button id="resetActivitiesBtn" class="btn-outline"><i class="fas fa-undo"></i> Reset All Progress</button></div>
        </div>
    </div>

    <!-- ZONAL SUMMARY PANEL -->
    <div id="zonalPanel" class="panel">
        <div class="card"><h2><i class="fas fa-globe"></i> Zonal Summary (by Godina/Zone)</h2><div id="zonalSummaryContainer"></div><canvas id="zonalChart" height="200" style="max-width:100%;"></canvas></div>
    </div>

    <!-- DASHBOARD PANEL -->
    <div id="dashboardPanel" class="panel">
        <div class="stats-grid" id="dashboardStats"></div>
        <div class="card"><h2><i class="fas fa-chart-pie"></i> Overall Progress</h2><canvas id="overallChart" height="150"></canvas></div>
        <div class="card"><h2><i class="fas fa-chart-bar"></i> Student Level Distribution (Current Phase)</h2><canvas id="studentChart" height="200"></canvas></div>
    </div>

    <!-- REPORT PANEL -->
    <div id="reportPanel" class="panel">
        <div class="card"><h2><i class="fas fa-file-alt"></i> Comprehensive Report</h2><div id="reportContent"></div><button id="printReportBtn" class="btn-outline" style="margin-top:16px;"><i class="fas fa-print"></i> Print Report</button></div>
    </div>
</div>

<script>
    // Student data with profile and phase assessments
    let students = [];
    let currentPhase = "baseline";
    // Activity data with Unit of Measurements and Target Plan
    let activities = [
        { code: "4.1.6", name: "Print TaRL teachers guideline & assessment tools", type: "Non-Training", unit: "Manuals", target: 864, achieved: 0 },
        { code: "4.2.6", name: "Print supplementary reading materials (SRMs)", type: "Non-Training", unit: "SRMs (Books)", target: 31400, achieved: 0 },
        { code: "4.2.7", name: "Procure SRMs book bank boxes/shelves", type: "Non-Training", unit: "Schools", target: 23, achieved: 0 },
        { code: "4.3", name: "Intra/inter-school reading & numeracy competitions", type: "Non-Training", unit: "Schools", target: 157, achieved: 0 },
        { code: "4.4.2", name: "Make classrooms & latrines accessible for CWDs", type: "Non-Training", unit: "Schools", target: 15, achieved: 0 },
        { code: "4.4.3", name: "Procure & distribute assistive devices for CWDs", type: "Non-Training", unit: "CWDs", target: 124, achieved: 0 },
        { code: "4.5", name: "Strengthen & establish reading clubs", type: "Non-Training", unit: "Schools", target: 157, achieved: 0 },
        { code: "4.5.1", name: "Training of Trainers (ToT) for master trainers", type: "Training", unit: "Master Trainers", target: 18, achieved: 0 },
        { code: "4.5.2", name: "Train teachers on TaRL & core reading skills", type: "Training", unit: "Teachers", target: 864, achieved: 0 },
        { code: "4.5.3", name: "Train model teachers & cluster supervisors as mentors", type: "Training", unit: "Mentors", target: 314, achieved: 0 },
        { code: "4.5.4", name: "Train school administrators & WEO experts", type: "Training", unit: "Personnel", target: 167, achieved: 0 },
        { code: "4.5.5", name: "Performance-based incentives", type: "Non-Training", unit: "Honorees", target: 236, achieved: 0 },
        { code: "4.5.6", name: "Conduct literacy skills assessment", type: "Training", unit: "Teachers", target: 864, achieved: 0 },
        { code: "4.6.1", name: "Multi-sectoral WASH training", type: "Training", unit: "Participants", target: 324, achieved: 0 },
        { code: "4.6.2a", name: "Media broadcast for SBCC", type: "Non-Training", unit: "Minutes", target: 60, achieved: 0 },
        { code: "4.6.2b", name: "Print banners, flyers, posters", type: "Non-Training", unit: "Schools", target: 157, achieved: 0 },
        { code: "4.6.2c", name: "Support mini-media clubs", type: "Non-Training", unit: "Schools", target: 157, achieved: 0 },
        { code: "4.8.1", name: "Orient gender club leaders", type: "Training", unit: "Participants", target: 471, achieved: 0 },
        { code: "4.8.2", name: "Train PTA, KETB, religious leaders", type: "Training", unit: "Participants", target: 544, achieved: 0 }
    ];

    const levelNames = { math: ['Jalqaba','D1','D2','Hirdhiisuu','Hiruu'], oromo: ['Jalqabdoota','Qubee','Jecha','Keey.Salphaa','Seeneessaa'], eng: ['Beginner','Letter','Word','Paragraph','Story'] };

    function loadData() {
        let s = localStorage.getItem("tarl_students_phases");
        if(s) students = JSON.parse(s);
        let a = localStorage.getItem("tarl_activities");
        if(a) { let saved = JSON.parse(a); for(let i=0;i<activities.length;i++) activities[i].achieved = saved[i]; }
        renderAll();
    }
    function saveData() {
        localStorage.setItem("tarl_students_phases", JSON.stringify(students));
        localStorage.setItem("tarl_activities", JSON.stringify(activities.map(a=>a.achieved)));
        renderAll();
    }

    function getBinaryArray(prefix) { let arr=[]; for(let i=0;i<=4;i++){ let chk=document.getElementById(prefix+i); arr.push(chk?.checked?1:0); } return arr; }
    function getHighestLevel(arr) { for(let i=4;i>=0;i--) if(arr[i]===1) return i; return 0; }

    function addStudent() {
        let zone=document.getElementById("regZone").value.trim(), woreda=document.getElementById("regWoreda").value.trim(), schoolId=document.getElementById("regSchoolId").value.trim(), school=document.getElementById("regSchoolName").value.trim(), name=document.getElementById("regFullName").value.trim(), grade=parseInt(document.getElementById("regGrade").value), gender=document.getElementById("regGender").value, special=document.getElementById("regSpecial").value;
        if(!name||!school){ alert("Fill Name and School"); return; }
        let math=getBinaryArray("regMath"), oromo=getBinaryArray("regOromo"), eng=getBinaryArray("regEng");
        let existing = students.find(s => s.school.toLowerCase()===school.toLowerCase() && s.name.toLowerCase()===name.toLowerCase());
        if(existing) {
            if(currentPhase==='baseline') existing.baseline = { math, oromo, eng };
            else if(currentPhase==='midline') existing.midline = { math, oromo, eng };
            else existing.endline = { math, oromo, eng };
            alert(`Assessment updated for ${currentPhase} phase`);
        } else {
            let newStudent = { id:Date.now(), zone, woreda, schoolId, school, name, grade, gender, special, baseline:null, midline:null, endline:null };
            if(currentPhase==='baseline') newStudent.baseline = { math, oromo, eng };
            else if(currentPhase==='midline') newStudent.midline = { math, oromo, eng };
            else newStudent.endline = { math, oromo, eng };
            students.push(newStudent);
            alert(`Student registered with ${currentPhase} assessment`);
        }
        saveData();
        document.getElementById("regFullName").value=""; document.getElementById("regSchoolName").value="";
        for(let i=0;i<=4;i++){ let m=document.getElementById("regMath"+i); if(m) m.checked=false; let o=document.getElementById("regOromo"+i); if(o) o.checked=false; let e=document.getElementById("regEng"+i); if(e) e.checked=false; }
    }

    function deleteStudent(id) { if(confirm("Delete student?")){ students=students.filter(s=>s.id!==id); saveData(); } }

    function getPhaseData(student, phase) { if(phase==='baseline') return student.baseline; if(phase==='midline') return student.midline; return student.endline; }

    function renderStudentTable() {
        let tbody=document.getElementById("studentBody"); if(!tbody) return;
        tbody.innerHTML="";
        students.forEach(s=>{
            let baseO = s.baseline ? levelNames.oromo[getHighestLevel(s.baseline.oromo)] : "-";
            let midO = s.midline ? levelNames.oromo[getHighestLevel(s.midline.oromo)] : "-";
            let endO = s.endline ? levelNames.oromo[getHighestLevel(s.endline.oromo)] : "-";
            tbody.innerHTML+=`<tr>
                <td><strong>${s.name}</strong><br><small>${s.zone||''} ${s.woreda||''}</small></td>
                <td>${s.school}<br><small>${s.grade}</small></td>
                <td>K${s.grade}</td><td>${s.gender}</td>
                <td>${baseO}</td><td>${midO}</td><td>${endO}</td>
                <td><button class="delete-student" data-id="${s.id}" style="background:#c23b22; padding:2px 8px;">Delete</button></td>
            </tr>`;
        });
        document.querySelectorAll('.delete-student').forEach(btn=>btn.addEventListener('click',()=>deleteStudent(parseInt(btn.getAttribute('data-id')))));
    }

    function renderActivitiesTable() {
        let tbody=document.getElementById("activitiesBody"); if(!tbody) return;
        tbody.innerHTML="";
        for(let i=0;i<activities.length;i++){
            let a=activities[i]; let percent=(a.achieved/a.target)*100; let status=percent>=100?"Completed":(percent>=75?"Advanced":(percent>=50?"In Progress":(percent>=25?"Partial":"Not Started")));
            let row=tbody.insertRow();
            row.insertCell(0).innerHTML=a.code;
            row.insertCell(1).innerHTML=a.name;
            row.insertCell(2).innerHTML=`<span class="badge" style="background:${a.type==='Training'?'#e8f3ef':'#fff1db'}">${a.type}</span>`;
            row.insertCell(3).innerHTML=`<span class="unit-badge">${a.unit}</span>`;
            row.insertCell(4).innerHTML=a.target.toLocaleString();
            let cell5=row.insertCell(5);
            let input=document.createElement("input"); input.type="number"; input.value=a.achieved; input.className="edit-input"; cell5.appendChild(input);
            row.insertCell(6).innerHTML=`<div class="progress-bar"><div class="progress-fill" style="width:${percent}%;"></div></div><span>${percent.toFixed(1)}%</span>`;
            row.insertCell(7).innerHTML=`<span class="badge ${status==='Completed'?'badge-success':(status==='In Progress'||status==='Advanced'?'badge-warning':'badge-info')}">${status}</span>`;
            let cell8=row.insertCell(8);
            let btn=document.createElement("button"); btn.innerHTML='<i class="fas fa-save"></i> Save'; btn.onclick=(function(idx, inp){ return function(){ let val=parseInt(inp.value); if(isNaN(val)) val=0; val=Math.min(activities[idx].target,Math.max(0,val)); if(confirm(`Update ${activities[idx].code} to ${val}?`)){ activities[idx].achieved=val; saveData(); } }; })(i, input);
            cell8.appendChild(btn);
        }
    }

    function renderZonalSummary() {
        let zones = [...new Set(students.map(s=>s.zone).filter(z=>z))];
        let html = `<div style="overflow-x:auto;"><table class="vertical-table"><thead><tr><th>Zone/Godina</th><th>Total Students</th><th>Baseline Oromo Avg</th><th>Midline Oromo Avg</th><th>Endline Oromo Avg</th><th>Story Level (Baseline)</th></tr></thead><tbody>`;
        let zoneData = [];
        for(let zone of zones){
            let zoneStudents = students.filter(s=>s.zone===zone);
            let total = zoneStudents.length;
            let baseAvg = zoneStudents.reduce((sum,s)=> sum + (s.baseline ? getHighestLevel(s.baseline.oromo) : 0),0)/total;
            let midAvg = zoneStudents.reduce((sum,s)=> sum + (s.midline ? getHighestLevel(s.midline.oromo) : 0),0)/total;
            let endAvg = zoneStudents.reduce((sum,s)=> sum + (s.endline ? getHighestLevel(s.endline.oromo) : 0),0)/total;
            let baseStory = zoneStudents.filter(s=>s.baseline && s.baseline.oromo[4]===1).length;
            html += `<tr><td><strong>${zone}</strong></td><td>${total}</td><td>${baseAvg.toFixed(1)}</td><td>${midAvg.toFixed(1)}</td><td>${endAvg.toFixed(1)}</td><td>${baseStory}</td></tr>`;
            zoneData.push({zone, total, baseAvg});
        }
        html += `</tbody></table></div>`;
        document.getElementById("zonalSummaryContainer").innerHTML = html;
        let ctx = document.getElementById('zonalChart')?.getContext('2d');
        if(ctx && zones.length){
            if(window.zonalChart) window.zonalChart.destroy();
            window.zonalChart = new Chart(ctx, { type: 'bar', data: { labels: zones, datasets: [{ label: 'Baseline Oromo Level', data: zoneData.map(z=>z.baseAvg), backgroundColor: '#1e5e48' }] } });
        }
    }

    function renderDashboard() {
        let totalTarget=activities.reduce((s,a)=>s+a.target,0);
        let totalAchieved=activities.reduce((s,a)=>s+a.achieved,0);
        let trainingAchieved=activities.filter(a=>a.type==="Training").reduce((s,a)=>s+a.achieved,0);
        let currentPhaseLearners = students.filter(s=>getPhaseData(s,currentPhase));
        let storyCount = currentPhaseLearners.filter(s=>getPhaseData(s,currentPhase)?.oromo[4]===1).length;
        document.getElementById("dashboardStats").innerHTML=`
            <div class="stat-card"><strong>📊 Overall Progress</strong><div class="stat-number">${((totalAchieved/totalTarget)*100).toFixed(1)}%</div></div>
            <div class="stat-card"><strong>👥 Training Achieved</strong><div class="stat-number">${trainingAchieved.toLocaleString()}</div></div>
            <div class="stat-card"><strong>🎓 Students (${currentPhase})</strong><div class="stat-number">${currentPhaseLearners.length}</div></div>
            <div class="stat-card"><strong>🏆 Story Level</strong><div class="stat-number">${storyCount}</div></div>`;
        let ctx=document.getElementById('overallChart')?.getContext('2d');
        if(ctx){ if(window.overallChart) window.overallChart.destroy(); window.overallChart=new Chart(ctx,{type:'doughnut',data:{labels:['Achieved','Remaining'],datasets:[{data:[totalAchieved,totalTarget-totalAchieved],backgroundColor:['#1e5e48','#e0ede5']}]}});}
        let levels=[0,0,0,0,0];
        currentPhaseLearners.forEach(s=>{ let d=getPhaseData(s,currentPhase); if(d) levels[getHighestLevel(d.oromo)]++;});
        let ctx2=document.getElementById('studentChart')?.getContext('2d');
        if(ctx2){ if(window.studentChart) window.studentChart.destroy(); window.studentChart=new Chart(ctx2,{type:'bar',data:{labels:levelNames.oromo,datasets:[{label:'Students at Level',data:levels,backgroundColor:'#ffcd6b'}]}});}
    }

    function renderReport() {
        let totalTarget=activities.reduce((s,a)=>s+a.target,0);
        let totalAchieved=activities.reduce((s,a)=>s+a.achieved,0);
        let zonalHtml = "";
        let zones = [...new Set(students.map(s=>s.zone).filter(z=>z))];
        for(let zone of zones){
            let zoneStudents = students.filter(s=>s.zone===zone);
            let baseStory = zoneStudents.filter(s=>s.baseline && s.baseline.oromo[4]===1).length;
            zonalHtml += `<li><strong>${zone}:</strong> ${zoneStudents.length} students, ${baseStory} at Story level</li>`;
        }
        document.getElementById("reportContent").innerHTML=`
            <h3>Oromia TaRL Program Report</h3>
            <p><strong>Date:</strong> ${new Date().toLocaleDateString()}</p>
            <p><strong>Overall Achievement:</strong> ${((totalAchieved/totalTarget)*100).toFixed(1)}% (${totalAchieved.toLocaleString()}/${totalTarget.toLocaleString()} units)</p>
            <p><strong>Total Students Registered:</strong> ${students.length}</p>
            <h4>Zonal Summary:</h4><ul>${zonalHtml || "<li>No zones data</li>"}</ul>
            <h4>Activities Summary:</h4>
            <table style="width:100%"><thead><tr><th>Type</th><th>Target</th><th>Achieved</th><th>%</th></tr></thead><tbody>
            <tr><td>Training Activities</td><td>${activities.filter(a=>a.type==="Training").reduce((s,a)=>s+a.target,0)}</td><td>${activities.filter(a=>a.type==="Training").reduce((s,a)=>s+a.achieved,0)}</td><td>${((activities.filter(a=>a.type==="Training").reduce((s,a)=>s+a.achieved,0)/activities.filter(a=>a.type==="Training").reduce((s,a)=>s+a.target,0))*100).toFixed(1)}%</td></tr>
            <tr><td>Non-Training Activities</td><td>${activities.filter(a=>a.type==="Non-Training").reduce((s,a)=>s+a.target,0)}</td><td>${activities.filter(a=>a.type==="Non-Training").reduce((s,a)=>s+a.achieved,0)}</td><td>${((activities.filter(a=>a.type==="Non-Training").reduce((s,a)=>s+a.achieved,0)/activities.filter(a=>a.type==="Non-Training").reduce((s,a)=>s+a.target,0))*100).toFixed(1)}%</td></tr>
            </tbody></table>`;
    }

    function exportStudentCSV() {
        let csv="Name,School,Grade,Gender,Zone,Woreda,BaselineOromo,MidlineOromo,EndlineOromo\n";
        students.forEach(s=>{
            let baseO=s.baseline?levelNames.oromo[getHighestLevel(s.baseline.oromo)]:"-";
            let midO=s.midline?levelNames.oromo[getHighestLevel(s.midline.oromo)]:"-";
            let endO=s.endline?levelNames.oromo[getHighestLevel(s.endline.oromo)]:"-";
            csv+=`"${s.name}","${s.school}",${s.grade},"${s.gender}","${s.zone||''}","${s.woreda||''}","${baseO}","${midO}","${endO}"\n`;
        });
        let blob=new Blob([csv],{type:"text/csv"}); let link=document.createElement("a"); link.href=URL.createObjectURL(blob); link.download="students_phases.csv"; link.click(); URL.revokeObjectURL(link.href);
    }

    function resetActivities() { if(confirm("Reset all activity progress?")){ for(let a of activities) a.achieved=0; saveData(); } }

    function createCheckboxes(containerId,prefix){ let c=document.getElementById(containerId); if(!c) return; let labels=containerId==='mathGroup'?['L0','L1','L2','L3','L4']:(containerId==='oromoGroup'?levelNames.oromo:levelNames.eng); c.innerHTML=''; for(let i=0;i<=4;i++){ c.innerHTML+=`<label class="binary-option"><input type="checkbox" id="${prefix}${i}"> <span>${labels[i]}</span></label>`; } }
    createCheckboxes('mathGroup','regMath'); createCheckboxes('oromoGroup','regOromo'); createCheckboxes('engGroup','regEng');

    document.getElementById("addStudentBtn")?.addEventListener("click", addStudent);
    document.getElementById("clearStudentBtn")?.addEventListener("click", ()=>{ document.getElementById("regFullName").value=""; document.getElementById("regSchoolName").value=""; document.getElementById("regZone").value=""; document.getElementById("regWoreda").value=""; document.getElementById("regSchoolId").value=""; for(let i=0;i<=4;i++){ let m=document.getElementById("regMath"+i); if(m) m.checked=false; let o=document.getElementById("regOromo"+i); if(o) o.checked=false; let e=document.getElementById("regEng"+i); if(e) e.checked=false; } });
    document.getElementById("exportStudentBtn")?.addEventListener("click", exportStudentCSV);
    document.getElementById("resetActivitiesBtn")?.addEventListener("click", resetActivities);
    document.getElementById("printReportBtn")?.addEventListener("click", ()=>window.print());
    
    document.querySelectorAll('.phase-btn').forEach(btn=>btn.addEventListener('click',function(){ document.querySelectorAll('.phase-btn').forEach(b=>b.classList.remove('active-phase')); this.classList.add('active-phase'); currentPhase=this.getAttribute('data-phase'); renderDashboard(); renderReport(); }));
    document.querySelectorAll('.nav-btn').forEach(btn=>btn.addEventListener('click',function(){ let pid=this.getAttribute('data-panel'); document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active')); this.classList.add('active'); document.querySelectorAll('.panel').forEach(p=>p.classList.remove('active-panel')); document.getElementById(pid).classList.add('active-panel'); if(pid==='dashboardPanel') renderDashboard(); if(pid==='activitiesPanel') renderActivitiesTable(); if(pid==='reportPanel') renderReport(); if(pid==='studentPanel') renderStudentTable(); if(pid==='zonalPanel') renderZonalSummary(); }));
    loadData();
</script>
</body>
</html>
