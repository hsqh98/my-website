<?php
// ==========================================
// 1. الاتصال بقاعدة البيانات (PHP)
// ==========================================
$host = "localhost";
$user = "root";     
$pass = "";         
$db   = "sixth_preparatory";

$conn = new mysqli($host, $user, $pass, $db);

if ($conn->connect_error) {
    die("فشل الاتصال بقاعدة البيانات: " . $conn->connect_error);
}

$conn->set_charset("utf8mb4");

// ==========================================
// 2. API لتأكيد الرمز المباشر النصي (AJAX)
// ==========================================
if (isset($_GET['action']) && $_GET['action'] === 'verify_passcode') {
    header('Content-Type: application/json; charset=utf-8');
    $paperId = (int)$_POST['paper_id'];
    $enteredCode = $_POST['passcode'] ?? '';

    $stmt = $conn->prepare("SELECT passcode FROM exam_papers WHERE id = ?");
    $stmt->bind_param("i", $paperId);
    $stmt->execute();
    $res = $stmt->get_result()->fetch_assoc();

    if ($res && !empty($res['passcode'])) {
        // المطابقة النصية المباشرة بدون تشفير
        if ($enteredCode === $res['passcode']) {
            echo json_encode(['success' => true]);
        } else {
            echo json_encode(['success' => false, 'message' => 'رمز العبور غير صحيح!']);
        }
    } else {
        echo json_encode(['success' => true]); // مسموح الدخول في حال لا يوجد رمز
    }
    exit;
}

// ==========================================
// 3. جلب الأسئلة مع كافة صفحات الأسئلة المتعددة والأجوبة
// ==========================================
$sql = "SELECT e.id, e.subject, e.branch, e.year, e.round, e.question_pdf,
        (e.passcode IS NOT NULL AND e.passcode != '') AS is_protected,
        GROUP_CONCAT(DISTINCT q.file_path SEPARATOR '||') AS questions_data,
        GROUP_CONCAT(DISTINCT CONCAT(a.id, '::', a.title, '::', a.file_path) SEPARATOR '||') AS answers_data
        FROM exam_papers e
        LEFT JOIN question_files q ON e.id = q.paper_id
        LEFT JOIN answer_files a ON e.id = a.paper_id
        GROUP BY e.id
        ORDER BY e.year DESC, e.id DESC";

$result = $conn->query($sql);
$papersData = [];

if ($result && $result->num_rows > 0) {
    while ($row = $result->fetch_assoc()) {
        $answers = [];
        if (!empty($row['answers_data'])) {
            $ansRaw = explode('||', $row['answers_data']);
            foreach ($ansRaw as $ans) {
                $parts = explode('::', $ans);
                if (count($parts) === 3) {
                    $answers[] = [
                        'id'    => $parts[0],
                        'title' => $parts[1],
                        'file'  => $parts[2]
                    ];
                }
            }
        }

        // جلب قائمة ملفات/صفحات الأسئلة
        $qPages = [];
        if (!empty($row['questions_data'])) {
            $qPages = explode('||', $row['questions_data']);
        } elseif (!empty($row['question_pdf'])) {
            $qPages[] = $row['question_pdf'];
        }

        $papersData[] = [
            'id'            => $row['id'],
            'subject'       => $row['subject'],
            'branch'        => $row['branch'],
            'year'          => (int)$row['year'],
            'round'         => $row['round'],
            'isProtected'   => (bool)$row['is_protected'],
            'questionPages' => $qPages,
            'answers'       => $answers
        ];
    }
}
?>
<!DOCTYPE html>
<html lang="ar" dir="rtl" data-theme="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>بنك أسئلة السادس العلمي - العراق</title>
    
    <!-- Google Fonts & FontAwesome -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800;900&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">

    <!-- CSS Styling -->
    <style>
        :root[data-theme="light"] {
            --bg-gradient: linear-gradient(135deg, #f0f4f8 0%, #e2e8f0 100%);
            --card-bg: rgba(255, 255, 255, 0.9);
            --card-border: rgba(255, 255, 255, 0.7);
            --text-main: #0f172a;
            --text-muted: #64748b;
            --primary: #10b981;
            --primary-hover: #059669;
            --secondary: #6366f1;
            --accent-glow: rgba(16, 185, 129, 0.15);
            --shadow-sm: 0 4px 6px -1px rgba(0,0,0,0.05);
            --shadow-lg: 0 15px 25px -5px rgba(0,0,0,0.08);
            --nav-bg: rgba(255, 255, 255, 0.85);
            --input-bg: #f8fafc;
            --close-btn-bg: #f1f5f9;
        }

        :root[data-theme="dark"] {
            --bg-gradient: linear-gradient(135deg, #0f172a 0%, #1e293b 100%);
            --card-bg: rgba(30, 41, 59, 0.85);
            --card-border: rgba(255, 255, 255, 0.08);
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --primary: #10b981;
            --primary-hover: #34d399;
            --secondary: #818cf8;
            --accent-glow: rgba(16, 185, 129, 0.25);
            --shadow-sm: 0 4px 6px -1px rgba(0,0,0,0.3);
            --shadow-lg: 0 20px 25px -5px rgba(0,0,0,0.5);
            --nav-bg: rgba(15, 23, 42, 0.85);
            --input-bg: #0f172a;
            --close-btn-bg: #334155;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            transition: background-color 0.25s ease, color 0.25s ease;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: 'Cairo', sans-serif;
            background: var(--bg-gradient);
            color: var(--text-main);
            min-height: 100vh;
            padding-bottom: 60px;
            overflow-x: hidden;
        }

        .container {
            width: 100%;
            max-width: 1250px;
            margin: 0 auto;
            padding: 0 16px;
        }

        .navbar {
            position: sticky;
            top: 0;
            z-index: 90;
            background: var(--nav-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border-bottom: 1px solid var(--card-border);
            padding: 12px 0;
        }

        .nav-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 1.15rem;
            font-weight: 800;
            color: var(--text-main);
            text-decoration: none;
        }

        .brand i {
            color: var(--primary);
            font-size: 1.4rem;
        }

        .nav-actions {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 6px;
            padding: 8px 14px;
            border-radius: 10px;
            font-family: 'Cairo';
            font-weight: 700;
            font-size: 0.85rem;
            border: none;
            cursor: pointer;
            text-decoration: none;
            white-space: nowrap;
        }

        .btn-primary {
            background: var(--primary);
            color: white;
            box-shadow: 0 4px 12px var(--accent-glow);
        }

        .btn-secondary {
            background: var(--card-bg);
            color: var(--text-main);
            border: 1px solid var(--card-border);
        }

        .theme-toggle {
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            color: var(--text-main);
            width: 38px;
            height: 38px;
            border-radius: 10px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1rem;
        }

        .hero {
            padding: 30px 0 20px;
            text-align: center;
        }

        .hero h1 {
            font-size: 1.8rem;
            font-weight: 900;
            margin-bottom: 8px;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .hero p {
            color: var(--text-muted);
            font-size: 0.95rem;
            max-width: 600px;
            margin: 0 auto;
            line-height: 1.5;
        }

        .glass-card {
            background: var(--card-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid var(--card-border);
            border-radius: 16px;
            padding: 20px;
            box-shadow: var(--shadow-lg);
            margin-bottom: 24px;
        }

        .section-title {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 1.1rem;
            font-weight: 800;
            margin-bottom: 16px;
            color: var(--text-main);
        }

        .section-title i {
            color: var(--primary);
        }

        .filter-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
        }

        .form-control {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }

        .form-control label {
            font-size: 0.8rem;
            font-weight: 700;
            color: var(--text-muted);
        }

        select, input[type="number"], input[type="text"], input[type="password"] {
            width: 100%;
            padding: 10px 12px;
            background: var(--input-bg);
            border: 1px solid var(--card-border);
            border-radius: 8px;
            color: var(--text-main);
            font-family: 'Cairo';
            font-size: 0.9rem;
            outline: none;
        }

        select:focus, input:focus {
            border-color: var(--primary);
        }

        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 16px;
        }

        .paper-card {
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            border-radius: 14px;
            padding: 16px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            position: relative;
            box-shadow: var(--shadow-sm);
        }

        .paper-card::before {
            content: '';
            position: absolute;
            top: 0; right: 0; left: 0;
            height: 4px;
            border-radius: 14px 14px 0 0;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
        }

        .paper-title {
            font-size: 1.05rem;
            font-weight: 800;
            margin-bottom: 10px;
        }

        .badge-group {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin-bottom: 16px;
        }

        .badge {
            background: var(--input-bg);
            color: var(--text-muted);
            border: 1px solid var(--card-border);
            padding: 3px 8px;
            border-radius: 6px;
            font-size: 0.75rem;
            font-weight: 700;
        }

        .badge-pages {
            background: rgba(99, 102, 241, 0.15);
            color: var(--secondary);
            border-color: var(--secondary);
        }

        .badge-protected {
            background: #fef2f2;
            color: #ef4444;
            border-color: #fca5a5;
        }

        .calc-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
            gap: 10px;
            margin-bottom: 16px;
        }

        .calc-box {
            background: var(--input-bg);
            padding: 10px;
            border-radius: 10px;
            border: 1px solid var(--card-border);
        }

        .calc-box label {
            display: block;
            font-size: 0.75rem;
            font-weight: 700;
            margin-bottom: 4px;
            color: var(--text-muted);
        }

        .calc-result-box {
            text-align: center;
            background: var(--accent-glow);
            border: 1px solid var(--primary);
            padding: 14px;
            border-radius: 12px;
            margin-top: 12px;
        }

        .calc-result-box h3 {
            font-size: 1.25rem;
            font-weight: 800;
            color: var(--primary);
        }

        .modal {
            display: none;
            position: fixed;
            top: 0; left: 0; right: 0; bottom: 0;
            width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(6px);
            -webkit-backdrop-filter: blur(6px);
            z-index: 1000;
            overflow-y: auto;
            padding: 12px;
        }

        .modal-container {
            width: 100%;
            max-width: 950px;
            margin: 10px auto;
            background: var(--card-bg);
            border: 1px solid var(--card-border);
            border-radius: 16px;
            padding: 18px;
            position: relative;
            box-shadow: var(--shadow-lg);
            display: flex;
            flex-direction: column;
        }

        .modal-footer {
            margin-top: 15px;
            padding-top: 12px;
            border-top: 1px solid var(--card-border);
            display: flex;
            justify-content: flex-end;
        }

        .btn-modal-close {
            background: var(--close-btn-bg);
            color: var(--text-main);
            border: 1px solid var(--card-border);
            padding: 10px 20px;
            border-radius: 8px;
            font-family: 'Cairo';
            font-weight: 700;
            font-size: 0.9rem;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            width: 100%;
            justify-content: center;
        }

        .modal-tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 16px;
            overflow-x: auto;
            padding-bottom: 6px;
            -webkit-overflow-scrolling: touch;
        }

        .tab-btn {
            padding: 8px 14px;
            border-radius: 8px;
            border: 1px solid var(--card-border);
            background: var(--input-bg);
            color: var(--text-main);
            font-family: 'Cairo';
            font-weight: 700;
            font-size: 0.82rem;
            cursor: pointer;
            white-space: nowrap;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            flex-shrink: 0;
        }

        .tab-btn.active {
            background: var(--primary);
            color: white;
            border-color: var(--primary);
        }

        .preview-viewer {
            width: 100%;
            min-height: 400px;
            display: flex;
            justify-content: center;
            align-items: center;
            background: var(--input-bg);
            border-radius: 10px;
            overflow: hidden;
            padding: 6px;
            position: relative;
        }

        .slide-nav-btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(0, 0, 0, 0.6);
            color: white;
            border: none;
            width: 44px;
            height: 44px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            cursor: pointer;
            z-index: 10;
        }

        .slide-prev { right: 10px; }
        .slide-next { left: 10px; }

        .preview-viewer:fullscreen,
        .preview-viewer:-webkit-full-screen {
            background: #0b132b;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .preview-viewer:fullscreen img,
        .preview-viewer:-webkit-full-screen img {
            max-height: 85vh !important;
        }

        .preview-viewer:fullscreen iframe,
        .preview-viewer:-webkit-full-screen iframe {
            height: 85vh !important;
        }

        .fs-nav-overlay {
            display: none;
        }

        .preview-viewer:fullscreen .fs-nav-overlay,
        .preview-viewer:-webkit-full-screen .fs-nav-overlay {
            display: flex;
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(15, 23, 42, 0.85);
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 10px 20px;
            border-radius: 30px;
            gap: 15px;
            align-items: center;
            backdrop-filter: blur(10px);
            z-index: 100;
        }

        .toast-container {
            position: fixed;
            bottom: 15px; left: 15px; right: 15px;
            z-index: 2000;
            display: flex;
            flex-direction: column;
            gap: 8px;
            pointer-events: none;
        }

        .toast {
            background: var(--card-bg);
            color: var(--text-main);
            border-right: 4px solid var(--primary);
            padding: 12px 16px;
            border-radius: 8px;
            box-shadow: var(--shadow-lg);
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 0.85rem;
            pointer-events: auto;
            animation: slideUp 0.3s ease;
        }

        .toast.error {
            border-right-color: #ef4444;
        }

        @keyframes slideUp {
            from { transform: translateY(100%); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        @media (max-width: 992px) {
            .filter-grid { grid-template-columns: repeat(2, 1fr); }
        }

        @media (max-width: 600px) {
            .hero h1 { font-size: 1.4rem; }
            .hero p { font-size: 0.85rem; }
            .filter-grid { grid-template-columns: 1fr; }
            .calc-grid { grid-template-columns: repeat(2, 1fr); }
            .cards-grid { grid-template-columns: 1fr; }
            .preview-viewer { min-height: 300px; }
            .preview-viewer iframe { height: 55vh !important; }
            .preview-viewer img { max-height: 50vh !important; }
        }
    </style>
</head>
<body>

    <!-- Toast Notifications Root -->
    <div class="toast-container" id="toastContainer"></div>

    <!-- Navigation Header -->
    <header class="navbar">
        <div class="container nav-content">
            <a href="#" class="brand">
                <i class="fa-solid fa-graduation-cap"></i>
                <span>السادس العلمي</span>
            </a>
            <div class="nav-actions">
                <button class="btn btn-secondary" onclick="openModal('calcModal')" title="حاسبة المعدل">
                    <i class="fa-solid fa-calculator"></i>
                    <span>حاسبة المعدل</span>
                </button>
                <button class="theme-toggle" id="themeToggle" onclick="toggleTheme()" title="تغيير المظهر">
                    <i class="fa-solid fa-moon"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Hero Header Section -->
    <section class="hero">
        <div class="container">
            <h1>بنك الأسئلة والحلول النموذجية الشامل</h1>
            <p>تصفح وحمل أسئلة السادس العلمي لجميع الأدوار والسنوات مع دعم التصفح الأفقي وملء الشاشة.</p>
        </div>
    </section>

    <!-- Main Content Area -->
    <main class="container">

        <!-- Search & Filter Section -->
        <section class="glass-card">
            <div class="section-title">
                <i class="fa-solid fa-sliders"></i>
                <span>تصفية وتحديد البحث</span>
            </div>
            <div class="filter-grid">
                <div class="form-control">
                    <label>المادة الدراسية</label>
                    <select id="filterSubject">
                        <option value="all">جميع المواد</option>
                        <option value="math">الرياضيات</option>
                        <option value="physics">الفيزياء</option>
                        <option value="chemistry">الكيمياء</option>
                        <option value="biology">الأحياء</option>
                        <option value="islamic">التربية الإسلامية</option>
                        <option value="arabic">اللغة العربية</option>
                        <option value="english">اللغة الإنكليزية</option>
                    </select>
                </div>
                <div class="form-control">
                    <label>الفرع الدراسي</label>
                    <select id="filterBranch">
                        <option value="all">جميع الفروع</option>
                        <option value="general">العلمي (عام)</option>
                        <option value="biology">الأحيائي</option>
                        <option value="application">التطبيقي</option>
                    </select>
                </div>
                <div class="form-control">
                    <label>السنة الدراسية</label>
                    <select id="filterYear">
                        <option value="all">جميع السنوات</option>
                        <?php for($y = 2026; $y >= 2013; $y--): ?>
                            <option value="<?= $y ?>"><?= $y ?></option>
                        <?php endfor; ?>
                    </select>
                </div>
                <div class="form-control">
                    <label>الدور الامتحاني</label>
                    <select id="filterRound">
                        <option value="all">جميع الأدوار</option>
                        <option value="round1">الدور الأول</option>
                        <option value="round2">الدور الثاني</option>
                        <option value="round3">الدور الثالث</option>
                        <option value="prelim">التمهيدي</option>
                        <option value="outside">خارج العراق</option>
                    </select>
                </div>
            </div>
        </section>

        <!-- Exam Papers Grid Display -->
        <section>
            <div class="cards-grid" id="papersGrid">
                <!-- Dynamic Javascript Cards -->
            </div>
        </section>
    </main>

    <!-- Modal Viewer (Lightbox) -->
    <div id="viewerModal" class="modal">
        <div class="modal-container">
            <div class="modal-tabs" id="modalTabsContainer"></div>
            <div class="preview-viewer" id="previewViewerArea">
                <button class="slide-nav-btn slide-prev" onclick="navigateSlide(-1)" title="الملف السابق"><i class="fa-solid fa-chevron-right"></i></button>
                <button class="slide-nav-btn slide-next" onclick="navigateSlide(1)" title="الملف التالي"><i class="fa-solid fa-chevron-left"></i></button>
                
                <div id="slideContent" style="width:100%; text-align:center;"></div>

                <div class="fs-nav-overlay">
                    <button class="btn btn-secondary" onclick="navigateSlide(-1)"><i class="fa-solid fa-chevron-right"></i> السابق</button>
                    <span id="fsSlideTitle" style="color:white; font-weight:700; font-size:0.9rem;">ورقة الأسئلة</span>
                    <button class="btn btn-secondary" onclick="navigateSlide(1)">التالي <i class="fa-solid fa-chevron-left"></i></button>
                    <button class="btn btn-primary" onclick="toggleFullscreen()"><i class="fa-solid fa-compress"></i> إنهاء ملء الشاشة</button>
                </div>
            </div>
            <div class="modal-footer">
                <button class="btn-modal-close" onclick="closeModal('viewerModal')">
                    <i class="fa-solid fa-xmark"></i> إغلاق ورقة الامتحان
                </button>
            </div>
        </div>
    </div>

    <!-- Modal Passcode Verification -->
    <div id="passcodeModal" class="modal">
        <div class="modal-container" style="max-width: 400px;">
            <div class="section-title">
                <i class="fa-solid fa-lock" style="color:#ef4444;"></i>
                <span>هذا النموذج مأمن برمز عبور</span>
            </div>
            <p style="font-size:0.85rem; color:var(--text-muted); margin-bottom:15px;">يرجى إدخال رمز العبور للفتح والاستعراض:</p>
            <input type="password" id="inputVerifyPasscode" placeholder="أدخل رمز العبور..." style="margin-bottom:15px;">
            <button class="btn btn-primary" style="width:100%; justify-content:center;" onclick="submitPasscodeVerification()">تأكيد وفتح الملف</button>
            <div class="modal-footer">
                <button class="btn-modal-close" onclick="closeModal('passcodeModal')">
                    <i class="fa-solid fa-xmark"></i> إلغاء
                </button>
            </div>
        </div>
    </div>

    <!-- Modal Grade Calculator -->
    <div id="calcModal" class="modal">
        <div class="modal-container">
            <div class="section-title">
                <i class="fa-solid fa-calculator"></i>
                <span>حاسبة معدل السادس العلمي التفاعلية</span>
            </div>
            <div class="calc-grid">
                <div class="calc-box"><label>التربية الإسلامية</label><input type="number" class="grade-input" placeholder="100"></div>
                <div class="calc-box"><label>اللغة العربية</label><input type="number" class="grade-input" placeholder="100"></div>
                <div class="calc-box"><label>اللغة الإنكليزية</label><input type="number" class="grade-input" placeholder="100"></div>
                <div class="calc-box"><label>الأحياء / الاقتصاد</label><input type="number" class="grade-input" placeholder="100"></div>
                <div class="calc-box"><label>الرياضيات</label><input type="number" class="grade-input" placeholder="100"></div>
                <div class="calc-box"><label>الكيمياء</label><input type="number" class="grade-input" placeholder="100"></div>
                <div class="calc-box"><label>الفيزياء</label><input type="number" class="grade-input" placeholder="100"></div>
            </div>
            <div style="display: flex; gap: 10px; align-items: center; margin-bottom: 15px;">
                <label style="cursor: pointer; font-weight:700; font-size:0.85rem;">
                    <input type="checkbox" id="addFirstRoundBonus" style="width:auto; margin-left:6px;"> إضافة درجة الدور الأول (+1)
                </label>
            </div>
            <button class="btn btn-primary" style="width: 100%; justify-content: center; padding: 12px;" onclick="calculateAverage()">حساب النتيجة والمعدل</button>
            <div class="calc-result-box" id="calcResultBox" style="display:none;">
                <h3 id="calcResultText">المعدل النهائي: 0.00%</h3>
            </div>
            <div class="modal-footer">
                <button class="btn-modal-close" onclick="closeModal('calcModal')">
                    <i class="fa-solid fa-xmark"></i> إغلاق الحاسبة
                </button>
            </div>
        </div>
    </div>

    <!-- JavaScript Interactive Logic -->
    <script>
        const papersData = <?= json_encode($papersData, JSON_UNESCAPED_UNICODE); ?>;
        let currentActivePaper = null;
        let activeSlideList = [];
        let currentSlideIndex = 0;
        let pendingPaperId = null;

        document.addEventListener("DOMContentLoaded", () => {
            renderGridCards(papersData);

            document.querySelectorAll(".filter-grid select").forEach(el => {
                el.addEventListener("change", applyFilters);
            });

            document.addEventListener("keydown", (e) => {
                if (document.getElementById("viewerModal").style.display === "block") {
                    if (e.key === "ArrowLeft") navigateSlide(1);
                    if (e.key === "ArrowRight") navigateSlide(-1);
                }
            });
        });

        function toggleTheme() {
            const currentTheme = document.documentElement.getAttribute("data-theme");
            const newTheme = currentTheme === "dark" ? "light" : "dark";
            document.documentElement.setAttribute("data-theme", newTheme);
            const icon = document.querySelector("#themeToggle i");
            icon.className = newTheme === "dark" ? "fa-solid fa-sun" : "fa-solid fa-moon";
        }

        function renderGridCards(data) {
            const grid = document.getElementById("papersGrid");
            grid.innerHTML = "";

            if (data.length === 0) {
                grid.innerHTML = `
                    <div style="grid-column: 1/-1; text-align:center; padding: 30px;" class="glass-card">
                        <i class="fa-solid fa-folder-open" style="font-size: 2rem; color: var(--text-muted); margin-bottom: 8px;"></i>
                        <p style="color: var(--text-muted); font-size: 0.9rem;">لا توجد نماذج امتحانية تطابق الفلترة.</p>
                    </div>
                `;
                return;
            }

            data.forEach(item => {
                const solutionsCount = item.answers ? item.answers.length : 0;
                const pagesCount = item.questionPages ? item.questionPages.length : 1;
                
                const card = document.createElement("div");
                card.className = "paper-card";
                card.innerHTML = `
                    <div>
                        <h3 class="paper-title">${getSubjectLabel(item.subject)}</h3>
                        <div class="badge-group">
                            <span class="badge"><i class="fa-regular fa-calendar"></i> ${item.year}</span>
                            <span class="badge">${getRoundLabel(item.round)}</span>
                            <span class="badge">${getBranchLabel(item.branch)}</span>
                            <span class="badge badge-pages"><i class="fa-solid fa-copy"></i> ${pagesCount} صفحات</span>
                            ${item.isProtected ? '<span class="badge badge-protected"><i class="fa-solid fa-lock"></i> محمي برمز</span>' : ''}
                        </div>
                    </div>
                    <button class="btn btn-primary" style="width:100%;" onclick="handleOpenViewer(${item.id})">
                        <i class="fa-solid ${item.isProtected ? 'fa-lock' : 'fa-eye'}"></i> عرض الأسئلة والحلول
                    </button>
                `;
                grid.appendChild(card);
            });
        }

        function applyFilters() {
            const subject = document.getElementById("filterSubject").value;
            const branch = document.getElementById("filterBranch").value;
            const year = document.getElementById("filterYear").value;
            const round = document.getElementById("filterRound").value;

            const filtered = papersData.filter(item => {
                return (subject === "all" || item.subject === subject) &&
                       (branch === "all" || item.branch === branch) &&
                       (year === "all" || item.year == year) &&
                       (round === "all" || item.round === round);
            });

            renderGridCards(filtered);
        }

        function openModal(id) {
            document.getElementById(id).style.display = "block";
            document.body.style.overflow = "hidden";
        }

        function closeModal(id) {
            document.getElementById(id).style.display = "none";
            document.body.style.overflow = "auto";
        }

        function handleOpenViewer(paperId) {
            const paper = papersData.find(p => p.id == paperId);
            if (!paper) return;

            if (paper.isProtected) {
                pendingPaperId = paperId;
                document.getElementById("inputVerifyPasscode").value = "";
                openModal("passcodeModal");
            } else {
                openViewer(paperId);
            }
        }

        async function submitPasscodeVerification() {
            const code = document.getElementById("inputVerifyPasscode").value;
            if (!code) {
                showToast("يرجى كتابة رمز العبور!", "error");
                return;
            }

            const formData = new FormData();
            formData.append("paper_id", pendingPaperId);
            formData.append("passcode", code);

            try {
                const res = await fetch("index.php?action=verify_passcode", {
                    method: "POST",
                    body: formData
                });
                const data = await res.json();

                if (data.success) {
                    closeModal("passcodeModal");
                    openViewer(pendingPaperId);
                    showToast("تم فتح الملف بنجاح!", "success");
                } else {
                    showToast(data.message || "رمز العبور غير صحيح!", "error");
                }
            } catch (err) {
                showToast("حدث خطأ في الاتصال بالسيرفر", "error");
            }
        }

        function openViewer(paperId) {
            currentActivePaper = papersData.find(p => p.id == paperId);
            if (!currentActivePaper) return;

            activeSlideList = [];

            // 1. إضافة صفحات الأسئلة أفقياً
            if (currentActivePaper.questionPages && currentActivePaper.questionPages.length > 0) {
                currentActivePaper.questionPages.forEach((qFile, idx) => {
                    activeSlideList.push({
                        title: `الأسئلة (صفحة ${idx + 1})`,
                        file: qFile
                    });
                });
            }

            // 2. إضافة نسخ الأجوبة النموذجية أفقياً
            if (currentActivePaper.answers && currentActivePaper.answers.length > 0) {
                currentActivePaper.answers.forEach(ans => {
                    activeSlideList.push({ title: ans.title, file: ans.file });
                });
            }

            openModal("viewerModal");
            
            const tabsContainer = document.getElementById("modalTabsContainer");
            tabsContainer.innerHTML = "";
            activeSlideList.forEach((slide, idx) => {
                tabsContainer.innerHTML += `
                    <button class="tab-btn ${idx === 0 ? 'active' : ''}" onclick="loadSlideIndex(${idx})">
                        <i class="fa-solid ${slide.title.includes('الأسئلة') ? 'fa-file-lines' : 'fa-check-double'}"></i> ${slide.title}
                    </button>
                `;
            });

            loadSlideIndex(0);
        }

        function loadSlideIndex(index) {
            if (index < 0 || index >= activeSlideList.length) return;
            currentSlideIndex = index;

            const buttons = document.querySelectorAll("#modalTabsContainer .tab-btn");
            buttons.forEach((b, i) => {
                if (i === index) b.classList.add("active");
                else b.classList.remove("active");
            });

            const slide = activeSlideList[index];
            const slideArea = document.getElementById("slideContent");
            document.getElementById("fsSlideTitle").innerText = slide.title;

            if (slide.file.toLowerCase().endsWith('.pdf')) {
                slideArea.innerHTML = `
                    <div style="width:100%; text-align:center;">
                        <iframe src="${slide.file}" style="width:100%; height:60vh; border:none; border-radius:6px;"></iframe>
                        <div style="margin-top:8px; display:flex; gap:10px; justify-content:center;">
                            <a href="${slide.file}" download class="btn btn-primary">
                                <i class="fa-solid fa-download"></i> تحميل الـ PDF
                            </a>
                            <button onclick="toggleFullscreen()" class="btn btn-secondary">
                                <i class="fa-solid fa-expand"></i> عرض ملء الشاشة
                            </button>
                        </div>
                    </div>
                `;
            } else {
                slideArea.innerHTML = `
                    <div style="text-align:center; width:100%;">
                        <img src="${slide.file}" style="max-width:100%; max-height:50vh; object-fit:contain; border-radius:6px; cursor:pointer;" onclick="toggleFullscreen()">
                        <div style="margin-top:12px; display:flex; gap:10px; justify-content:center;">
                            <a href="${slide.file}" download class="btn btn-primary">
                                <i class="fa-solid fa-download"></i> تحميل الصورة
                            </a>
                            <button onclick="toggleFullscreen()" class="btn btn-secondary">
                                <i class="fa-solid fa-expand"></i> عرض ملء الشاشة
                            </button>
                        </div>
                    </div>
                `;
            }
        }

        function navigateSlide(direction) {
            let nextIndex = currentSlideIndex + direction;
            if (nextIndex >= activeSlideList.length) nextIndex = 0;
            if (nextIndex < 0) nextIndex = activeSlideList.length - 1;
            loadSlideIndex(nextIndex);
        }

        function toggleFullscreen() {
            const element = document.getElementById("previewViewerArea");
            if (!document.fullscreenElement && !document.webkitFullscreenElement) {
                if (element.requestFullscreen) {
                    element.requestFullscreen();
                } else if (element.webkitRequestFullscreen) {
                    element.webkitRequestFullscreen();
                }
            } else {
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                } else if (document.webkitExitFullscreen) {
                    document.webkitExitFullscreen();
                }
            }
        }

        function calculateAverage() {
            const inputs = document.querySelectorAll("#calcModal .grade-input");
            let sum = 0, count = 0;

            inputs.forEach(input => {
                const val = parseFloat(input.value);
                if (!isNaN(val)) {
                    sum += val;
                    count++;
                }
            });

            if (count === 0) {
                showToast("يرجى إدخال درجات مادة واحدة على الأقل", "error");
                return;
            }

            let avg = sum / count;
            if (document.getElementById("addFirstRoundBonus").checked) {
                avg += 1;
            }

            const resultBox = document.getElementById("calcResultBox");
            document.getElementById("calcResultText").innerText = `المعدل النهائي: ${avg.toFixed(2)}%`;
            resultBox.style.display = "block";
            showToast("تم حساب المعدل بنجاح", "success");
        }

        function showToast(message, type = "success") {
            const container = document.getElementById("toastContainer");
            const toast = document.createElement("div");
            toast.className = `toast ${type}`;
            toast.innerHTML = `
                <i class="fa-solid ${type === 'success' ? 'fa-circle-check' : 'fa-circle-exclamation'}"></i>
                <span>${message}</span>
            `;
            container.appendChild(toast);

            setTimeout(() => {
                toast.style.opacity = '0';
                setTimeout(() => toast.remove(), 300);
            }, 3500);
        }

        function getSubjectLabel(code) {
            const m = { math: "الرياضيات", physics: "الفيزياء", chemistry: "الكيمياء", biology: "الأحياء", islamic: "التربية الإسلامية", arabic: "اللغة العربية", english: "اللغة الإنكليزية" };
            return m[code] || code;
        }

        function getRoundLabel(code) {
            const m = { round1: "الدور الأول", round2: "الدور الثاني", round3: "الدور الثالث", prelim: "التمهيدي", outside: "خارج العراق" };
            return m[code] || code;
        }

        function getBranchLabel(code) {
            const m = { general: "العلمي", biology: "الأحيائي", application: "التطبيقي" };
            return m[code] || code;
        }
    </script>
</body>
</html>