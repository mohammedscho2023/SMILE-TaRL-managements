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
