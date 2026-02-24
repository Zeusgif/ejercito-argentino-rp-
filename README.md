# ejercito-argentino-rp-
Página oficial del ejército argentino RP (servidor Guerra Mundial RP)
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ejército Argentino - Sistema de Gestión</title>
    <link href="https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@300;400;600;700&family=Roboto+Mono:wght@400;500&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4a7c59;
            --primary-dark: #2d4a35;
            --secondary: #8b9a46;
            --accent: #d4af37;
            --dark: #1a1f1a;
            --darker: #0f120f;
            --light: #e8ece8;
            --danger: #8b2635;
            --warning: #c9a227;
            --success: #4a7c59;
            --glass: rgba(26, 31, 26, 0.95);
            --border: rgba(139, 154, 70, 0.3);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Chakra Petch', sans-serif;
            background: var(--darker);
            color: var(--light);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Background Pattern */
        .bg-pattern {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(74, 124, 89, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(74, 124, 89, 0.03) 1px, transparent 1px);
            background-size: 50px 50px;
            pointer-events: none;
            z-index: 0;
        }

        /* Login Screen */
        .login-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--darker) 0%, var(--dark) 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            transition: opacity 0.5s ease, visibility 0.5s;
        }

        .login-screen.hidden {
            opacity: 0;
            visibility: hidden;
        }

        .login-container {
            background: var(--glass);
            border: 1px solid var(--border);
            padding: 3rem;
            border-radius: 4px;
            width: 90%;
            max-width: 450px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.5);
            position: relative;
            overflow: hidden;
        }

        .login-container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary), var(--accent), var(--primary));
        }

        .logo-section {
            text-align: center;
            margin-bottom: 2rem;
        }

        .logo {
            width: 100px;
            height: 100px;
            background: var(--primary);
            border-radius: 50%;
            margin: 0 auto 1rem;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5rem;
            border: 3px solid var(--accent);
            box-shadow: 0 0 30px rgba(212, 175, 55, 0.3);
        }

        .login-container h1 {
            color: var(--accent);
            font-size: 1.8rem;
            letter-spacing: 2px;
            margin-bottom: 0.5rem;
        }

        .login-container p {
            color: var(--secondary);
            font-size: 0.9rem;
        }

        .form-group {
            margin-bottom: 1.5rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            color: var(--secondary);
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 0.8rem;
            background: rgba(0,0,0,0.3);
            border: 1px solid var(--border);
            color: var(--light);
            font-family: 'Roboto Mono', monospace;
            border-radius: 3px;
            transition: all 0.3s;
        }

        .form-group input:focus, .form-group select:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 10px rgba(212, 175, 55, 0.2);
        }

        .btn {
            width: 100%;
            padding: 1rem;
            background: linear-gradient(135deg, var(--primary) 0%, var(--primary-dark) 100%);
            border: 1px solid var(--accent);
            color: white;
            font-family: 'Chakra Petch', sans-serif;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 2px;
            cursor: pointer;
            border-radius: 3px;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 20px rgba(74, 124, 89, 0.4);
        }

        .btn:active {
            transform: translateY(0);
        }

        /* Main Layout */
        .main-app {
            display: none;
            min-height: 100vh;
        }

        .main-app.active {
            display: flex;
        }

        /* Sidebar */
        .sidebar {
            width: 280px;
            background: var(--dark);
            border-right: 1px solid var(--border);
            padding: 2rem 0;
            position: fixed;
            height: 100vh;
            overflow-y: auto;
            z-index: 100;
        }

        .sidebar-header {
            padding: 0 2rem 2rem;
            border-bottom: 1px solid var(--border);
            margin-bottom: 2rem;
        }

        .sidebar-header h2 {
            color: var(--accent);
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .user-info {
            margin-top: 1rem;
            padding: 1rem;
            background: rgba(0,0,0,0.2);
            border-radius: 4px;
            border-left: 3px solid var(--accent);
        }

        .user-rank {
            font-size: 0.75rem;
            color: var(--secondary);
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .user-name {
            font-weight: 600;
            color: var(--light);
            margin-top: 0.2rem;
        }

        .nav-menu {
            list-style: none;
            padding: 0 1rem;
        }

        .nav-item {
            margin-bottom: 0.5rem;
        }

        .nav-link {
            display: flex;
            align-items: center;
            gap: 1rem;
            padding: 1rem 1.5rem;
            color: var(--light);
            text-decoration: none;
            border-radius: 4px;
            transition: all 0.3s;
            cursor: pointer;
            border-left: 3px solid transparent;
        }

        .nav-link:hover, .nav-link.active {
            background: rgba(74, 124, 89, 0.1);
            border-left-color: var(--accent);
            color: var(--accent);
        }

        .nav-link i {
            width: 24px;
            text-align: center;
        }

        /* Content Area */
        .content {
            margin-left: 280px;
            flex: 1;
            padding: 2rem;
            position: relative;
            z-index: 1;
        }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
            padding-bottom: 1rem;
            border-bottom: 1px solid var(--border);
        }

        .header h1 {
            font-size: 2rem;
            color: var(--light);
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .header-actions {
            display: flex;
            gap: 1rem;
        }

        .btn-secondary {
            padding: 0.6rem 1.2rem;
            background: transparent;
            border: 1px solid var(--border);
            color: var(--light);
            cursor: pointer;
            border-radius: 3px;
            font-family: 'Chakra Petch', sans-serif;
            transition: all 0.3s;
        }

        .btn-secondary:hover {
            border-color: var(--accent);
            color: var(--accent);
        }

        .btn-primary {
            padding: 0.6rem 1.2rem;
            background: var(--primary);
            border: 1px solid var(--primary);
            color: white;
            cursor: pointer;
            border-radius: 3px;
            font-family: 'Chakra Petch', sans-serif;
            transition: all 0.3s;
        }

        .btn-primary:hover {
            background: var(--primary-dark);
        }

        /* Sections */
        .section {
            display: none;
            animation: fadeIn 0.5s;
        }

        .section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Cards */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1.5rem;
            margin-bottom: 2rem;
        }

        .stat-card {
            background: var(--dark);
            border: 1px solid var(--border);
            padding: 1.5rem;
            border-radius: 4px;
            position: relative;
            overflow: hidden;
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 4px;
            height: 100%;
            background: var(--accent);
        }

        .stat-label {
            color: var(--secondary);
            font-size: 0.85rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 0.5rem;
        }

        .stat-value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--light);
        }

        .stat-change {
            font-size: 0.85rem;
            margin-top: 0.5rem;
            color: var(--success);
        }

        /* Tables */
        .data-table {
            width: 100%;
            background: var(--dark);
            border: 1px solid var(--border);
            border-radius: 4px;
            overflow: hidden;
        }

        .table-header {
            display: grid;
            grid-template-columns: 80px 2fr 1fr 1fr 1fr 120px;
            padding: 1rem;
            background: rgba(0,0,0,0.2);
            border-bottom: 1px solid var(--border);
            font-weight: 600;
            color: var(--accent);
            text-transform: uppercase;
            font-size: 0.8rem;
            letter-spacing: 1px;
        }

        .table-row {
            display: grid;
            grid-template-columns: 80px 2fr 1fr 1fr 1fr 120px;
            padding: 1rem;
            border-bottom: 1px solid var(--border);
            align-items: center;
            transition: background 0.3s;
        }

        .table-row:hover {
            background: rgba(74, 124, 89, 0.05);
        }

        .table-row:last-child {
            border-bottom: none;
        }

        .rank-badge {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            width: 40px;
            height: 40px;
            background: var(--primary);
            border-radius: 50%;
            font-weight: 700;
            font-size: 0.8rem;
            border: 2px solid var(--accent);
        }

        .status-badge {
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: 600;
        }

        .status-active {
            background: rgba(74, 124, 89, 0.2);
            color: var(--success);
            border: 1px solid var(--success);
        }

        .status-inactive {
            background: rgba(139, 38, 53, 0.2);
            color: var(--danger);
            border: 1px solid var(--danger);
        }

        .actions {
            display: flex;
            gap: 0.5rem;
        }

        .btn-icon {
            width: 32px;
            height: 32px;
            border: 1px solid var(--border);
            background: transparent;
            color: var(--light);
            cursor: pointer;
            border-radius: 3px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s;
        }

        .btn-icon:hover {
            border-color: var(--accent);
            color: var(--accent);
            transform: scale(1.1);
        }

        .btn-icon.delete:hover {
            border-color: var(--danger);
            color: var(--danger);
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 1000;
            align-items: center;
            justify-content: center;
            backdrop-filter: blur(5px);
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: var(--dark);
            border: 1px solid var(--border);
            width: 90%;
            max-width: 600px;
            border-radius: 4px;
            max-height: 90vh;
            overflow-y: auto;
            animation: slideUp 0.3s;
        }

        @keyframes slideUp {
            from { transform: translateY(50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .modal-header {
            padding: 1.5rem;
            border-bottom: 1px solid var(--border);
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: rgba(0,0,0,0.2);
        }

        .modal-header h2 {
            color: var(--accent);
            font-size: 1.3rem;
        }

        .close-btn {
            background: none;
            border: none;
            color: var(--light);
            font-size: 1.5rem;
            cursor: pointer;
            transition: color 0.3s;
        }

        .close-btn:hover {
            color: var(--danger);
        }

        .modal-body {
            padding: 1.5rem;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 1rem;
        }

        .form-group {
            margin-bottom: 1rem;
        }

        .form-group.full {
            grid-column: 1 / -1;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            color: var(--secondary);
            font-size: 0.85rem;
            text-transform: uppercase;
        }

        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 0.8rem;
            background: rgba(0,0,0,0.3);
            border: 1px solid var(--border);
            color: var(--light);
            font-family: 'Roboto Mono', monospace;
            border-radius: 3px;
        }

        .form-group textarea {
            resize: vertical;
            min-height: 100px;
        }

        .modal-footer {
            padding: 1rem 1.5rem;
            border-top: 1px solid var(--border);
            display: flex;
            justify-content: flex-end;
            gap: 1rem;
            background: rgba(0,0,0,0.2);
        }

        /* Laws Section */
        .law-card {
            background: var(--dark);
            border: 1px solid var(--border);
            border-radius: 4px;
            padding: 1.5rem;
            margin-bottom: 1rem;
            position: relative;
            padding-left: 3rem;
        }

        .law-number {
            position: absolute;
            left: 1rem;
            top: 1.5rem;
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--accent);
            opacity: 0.5;
        }

        .law-title {
            font-size: 1.1rem;
            color: var(--light);
            margin-bottom: 0.5rem;
            font-weight: 600;
        }

        .law-content {
            color: var(--secondary);
            line-height: 1.6;
            font-size: 0.95rem;
        }

        .law-meta {
            margin-top: 1rem;
            padding-top: 1rem;
            border-top: 1px solid var(--border);
            display: flex;
            gap: 2rem;
            font-size: 0.85rem;
            color: var(--secondary);
        }

        /* Announcements */
        .announcement-card {
            background: var(--dark);
            border: 1px solid var(--border);
            border-radius: 4px;
            padding: 1.5rem;
            margin-bottom: 1rem;
            border-left: 4px solid var(--accent);
        }

        .announcement-header {
            display: flex;
            justify-content: space-between;
            align-items: start;
            margin-bottom: 1rem;
        }

        .announcement-title {
            font-size: 1.2rem;
            color: var(--light);
            margin-bottom: 0.3rem;
        }

        .announcement-date {
            font-size: 0.85rem;
            color: var(--secondary);
            font-family: 'Roboto Mono', monospace;
        }

        .announcement-priority {
            padding: 0.3rem 0.8rem;
            border-radius: 3px;
            font-size: 0.75rem;
            text-transform: uppercase;
            font-weight: 600;
        }

        .priority-high {
            background: var(--danger);
            color: white;
        }

        .priority-medium {
            background: var(--warning);
            color: var(--dark);
        }

        .priority-low {
            background: var(--primary);
            color: white;
        }

        .announcement-content {
            color: var(--secondary);
            line-height: 1.6;
        }

        /* Ranks Display */
        .ranks-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 1.5rem;
        }

        .rank-card {
            background: var(--dark);
            border: 1px solid var(--border);
            border-radius: 4px;
            padding: 1.5rem;
            text-align: center;
            transition: all 0.3s;
            position: relative;
            overflow: hidden;
        }

        .rank-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--primary), var(--accent));
        }

        .rank-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            border-color: var(--accent);
        }

        .rank-insignia {
            width: 80px;
            height: 80px;
            background: linear-gradient(135deg, var(--primary) 0%, var(--primary-dark) 100%);
            border-radius: 50%;
            margin: 0 auto 1rem;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            border: 3px solid var(--accent);
            box-shadow: 0 0 20px rgba(212, 175, 55, 0.2);
        }

        .rank-name {
            font-size: 1.2rem;
            color: var(--light);
            margin-bottom: 0.5rem;
            font-weight: 600;
        }

        .rank-level {
            color: var(--accent);
            font-size: 0.9rem;
            margin-bottom: 1rem;
        }

        .rank-description {
            color: var(--secondary);
            font-size: 0.9rem;
            line-height: 1.5;
        }

        /* Responsive */
        @media (max-width: 768px) {
            .sidebar {
                transform: translateX(-100%);
                transition: transform 0.3s;
            }
            
            .sidebar.open {
                transform: translateX(0);
            }
            
            .content {
                margin-left: 0;
            }
            
            .table-header, .table-row {
                grid-template-columns: 60px 1fr 1fr;
                font-size: 0.9rem;
            }
            
            .table-header > *:nth-child(4),
            .table-header > *:nth-child(5),
            .table-row > *:nth-child(4),
            .table-row > *:nth-child(5) {
                display: none;
            }
        }

        /* Toast Notifications */
        .toast-container {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 2000;
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .toast {
            background: var(--dark);
            border: 1px solid var(--border);
            border-left: 4px solid var(--accent);
            padding: 1rem 1.5rem;
            border-radius: 4px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.3);
            animation: slideInRight 0.3s;
            min-width: 300px;
        }

        .toast.success {
            border-left-color: var(--success);
        }

        .toast.error {
            border-left-color: var(--danger);
        }

        @keyframes slideInRight {
            from { transform: translateX(100%); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        /* Search Box */
        .search-box {
            position: relative;
            margin-bottom: 1.5rem;
        }

        .search-box input {
            width: 100%;
            padding: 1rem 1rem 1rem 3rem;
            background: var(--dark);
            border: 1px solid var(--border);
            color: var(--light);
            font-family: 'Roboto Mono', monospace;
            border-radius: 4px;
        }

        .search-box::before {
            content: '🔍';
            position: absolute;
            left: 1rem;
            top: 50%;
            transform: translateY(-50%);
            opacity: 0.5;
        }

        /* Empty State */
        .empty-state {
            text-align: center;
            padding: 3rem;
            color: var(--secondary);
        }

        .empty-state-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
            opacity: 0.5;
        }

        /* Print Styles */
        @media print {
            .sidebar, .header-actions, .btn-icon {
                display: none !important;
            }
            
            .content {
                margin-left: 0;
            }
        }
    </style>
</head>
<body>
    <div class="bg-pattern"></div>

    <!-- Login Screen -->
    <div class="login-screen" id="loginScreen">
        <div class="login-container">
            <div class="logo-section">
                <div class="logo">⚔️</div>
                <h1>EJÉRCITO ARGENTINO</h1>
                <p>Sistema de Gestión Militar</p>
            </div>
            <form id="loginForm">
                <div class="form-group">
                    <label>Usuario</label>
                    <input type="text" id="username" required placeholder="Ingrese su usuario">
                </div>
                <div class="form-group">
                    <label>Contraseña</label>
                    <input type="password" id="password" required placeholder="••••••••">
                </div>
                <div class="form-group">
                    <label>Unidad</label>
                    <select id="unit">
                        <option value="Comando General">Comando General</option>
                        <option value="I Brigada">I Brigada de Infantería</option>
                        <option value="II Brigada">II Brigada de Caballería</option>
                        <option value="III Brigada">III Brigada de Artillería</option>
                        <option value="IV Brigada">IV Brigada de Ingenieros</option>
                        <option value="Fuerza Aérea">Fuerza Aérea</option>
                    </select>
                </div>
                <button type="submit" class="btn">Iniciar Sesión</button>
            </form>
        </div>
    </div>

    <!-- Main Application -->
    <div class="main-app" id="mainApp">
        <!-- Sidebar -->
        <aside class="sidebar">
            <div class="sidebar-header">
                <h2>⚔️ EA Command</h2>
                <div class="user-info">
                    <div class="user-rank" id="userRank">General de División</div>
                    <div class="user-name" id="userDisplayName">Admin Principal</div>
                </div>
            </div>
            <nav>
                <ul class="nav-menu">
                    <li class="nav-item">
                        <a class="nav-link active" onclick="showSection('dashboard')">
                            <i>📊</i> Dashboard
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" onclick="showSection('members')">
                            <i>👥</i> Miembros
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" onclick="showSection('ranks')">
                            <i>⭐</i> Rangos
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" onclick="showSection('laws')">
                            <i>📜</i> Leyes y Reglas
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" onclick="showSection('announcements')">
                            <i>📢</i> Anuncios
                        </a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" onclick="logout()">
                            <i>🚪</i> Cerrar Sesión
                        </a>
                    </li>
                </ul>
            </nav>
        </aside>

        <!-- Content -->
        <main class="content">
            <!-- Dashboard Section -->
            <section class="section active" id="dashboard">
                <div class="header">
                    <h1>Dashboard</h1>
                    <div class="header-actions">
                        <button class="btn-secondary" onclick="refreshData()">🔄 Actualizar</button>
                    </div>
                </div>
                
                <div class="stats-grid">
                    <div class="stat-card">
                        <div class="stat-label">Total de Miembros</div>
                        <div class="stat-value" id="totalMembers">0</div>
                        <div class="stat-change">↑ 12% este mes</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Unidades Activas</div>
                        <div class="stat-value">6</div>
                        <div class="stat-change">Operativas</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Anuncios Pendientes</div>
                        <div class="stat-value" id="pendingAnnouncements">0</div>
                        <div class="stat-change">Requieren atención</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-label">Leyes Vigentes</div>
                        <div class="stat-value" id="totalLaws">0</div>
                        <div class="stat-change">Regulaciones activas</div>
                    </div>
                </div>

                <div style="background: var(--dark); border: 1px solid var(--border); border-radius: 4px; padding: 2rem;">
                    <h3 style="color: var(--accent); margin-bottom: 1rem;">📈 Actividad Reciente</h3>
                    <div id="recentActivity">
                        <div class="empty-state">
                            <div class="empty-state-icon">📋</div>
                            <p>No hay actividad reciente para mostrar</p>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Members Section -->
            <section class="section" id="members">
                <div class="header">
                    <h1>Gestión de Miembros</h1>
                    <div class="header-actions">
                        <button class="btn-primary" onclick="openModal('memberModal')">+ Nuevo Miembro</button>
                    </div>
                </div>

                <div class="search-box">
                    <input type="text" id="searchMembers" placeholder="Buscar por nombre, rango o unidad..." onkeyup="filterMembers()">
                </div>

                <div class="data-table">
                    <div class="table-header">
                        <div>Rango</div>
                        <div>Nombre</div>
                        <div>Unidad</div>
                        <div>Especialidad</div>
                        <div>Estado</div>
                        <div>Acciones</div>
                    </div>
                    <div id="membersTableBody">
                        <!-- Dynamic content -->
                    </div>
                </div>
            </section>

            <!-- Ranks Section -->
            <section class="section" id="ranks">
                <div class="header">
                    <h1>Jerarquía de Rangos</h1>
                    <div class="header-actions">
                        <button class="btn-primary" onclick="openModal('rankModal')">+ Agregar Rango</button>
                    </div>
                </div>

                <div class="ranks-grid" id="ranksGrid">
                    <!-- Dynamic content -->
                </div>
            </section>

            <!-- Laws Section -->
            <section class="section" id="laws">
                <div class="header">
                    <h1>Código Militar</h1>
                    <div class="header-actions">
                        <button class="btn-primary" onclick="openModal('lawModal')">+ Nueva Ley</button>
                    </div>
                </div>

                <div id="lawsContainer">
                    <!-- Dynamic content -->
                </div>
            </section>

            <!-- Announcements Section -->
            <section class="section" id="announcements">
                <div class="header">
                    <h1>Anuncios Oficiales</h1>
                    <div class="header-actions">
                        <button class="btn-primary" onclick="openModal('announcementModal')">+ Nuevo Anuncio</button>
                    </div>
                </div>

                <div id="announcementsContainer">
                    <!-- Dynamic content -->
                </div>
            </section>
        </main>
    </div>

    <!-- Modals -->
    <!-- Member Modal -->
    <div class="modal" id="memberModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="memberModalTitle">Nuevo Miembro</h2>
                <button class="close-btn" onclick="closeModal('memberModal')">&times;</button>
            </div>
            <div class="modal-body">
                <form id="memberForm">
                    <input type="hidden" id="memberId">
                    <div class="form-row">
                        <div class="form-group">
                            <label>Nombre Completo</label>
                            <input type="text" id="memberName" required>
                        </div>
                        <div class="form-group">
                            <label>Rango</label>
                            <select id="memberRank" required>
                                <!-- Dynamic options -->
                            </select>
                        </div>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label>Unidad</label>
                            <select id="memberUnit" required>
                                <option value="Comando General">Comando General</option>
                                <option value="I Brigada">I Brigada de Infantería</option>
                                <option value="II Brigada">II Brigada de Caballería</option>
                                <option value="III Brigada">III Brigada de Artillería</option>
                                <option value="IV Brigada">IV Brigada de Ingenieros</option>
                                <option value="Fuerza Aérea">Fuerza Aérea</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Especialidad</label>
                            <input type="text" id="memberSpecialty" placeholder="Ej: Comunicaciones, Médico, etc.">
                        </div>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label>Fecha de Ingreso</label>
                            <input type="date" id="memberDate" required>
                        </div>
                        <div class="form-group">
                            <label>Estado</label>
                            <select id="memberStatus">
                                <option value="Activo">Activo</option>
                                <option value="Inactivo">Inactivo</option>
                                <option value="Licencia">Licencia</option>
                            </select>
                        </div>
                    </div>
                </form>
            </div>
            <div class="modal-footer">
                <button class="btn-secondary" onclick="closeModal('memberModal')">Cancelar</button>
                <button class="btn-primary" onclick="saveMember()">Guardar</button>
            </div>
        </div>
    </div>

    <!-- Rank Modal -->
    <div class="modal" id="rankModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="rankModalTitle">Nuevo Rango</h2>
                <button class="close-btn" onclick="closeModal('rankModal')">&times;</button>
            </div>
            <div class="modal-body">
                <form id="rankForm">
                    <input type="hidden" id="rankId">
                    <div class="form-row">
                        <div class="form-group">
                            <label>Nombre del Rango</label>
                            <input type="text" id="rankName" required>
                        </div>
                        <div class="form-group">
                            <label>Nivel Jerárquico</label>
                            <input type="number" id="rankLevel" min="1" max="20" required>
                        </div>
                    </div>
                    <div class="form-group full">
                        <label>Descripción</label>
                        <textarea id="rankDescription" placeholder="Funciones y responsabilidades..."></textarea>
                    </div>
                    <div class="form-group">
                        <label>Insignia (Emoji o Texto)</label>
                        <input type="text" id="rankInsignia" placeholder="Ej: ⭐, 🎖️, etc." maxlength="2">
                    </div>
                </form>
            </div>
            <div class="modal-footer">
                <button class="btn-secondary" onclick="closeModal('rankModal')">Cancelar</button>
                <button class="btn-primary" onclick="saveRank()">Guardar</button>
            </div>
        </div>
    </div>

    <!-- Law Modal -->
    <div class="modal" id="lawModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="lawModalTitle">Nueva Ley</h2>
                <button class="close-btn" onclick="closeModal('lawModal')">&times;</button>
            </div>
            <div class="modal-body">
                <form id="lawForm">
                    <input type="hidden" id="lawId">
                    <div class="form-group">
                        <label>Título de la Ley</label>
                        <input type="text" id="lawTitle" required>
                    </div>
                    <div class="form-group">
                        <label>Contenido</label>
                        <textarea id="lawContent" rows="6" required placeholder="Artículos y disposiciones..."></textarea>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label>Categoría</label>
                            <select id="lawCategory">
                                <option value="Disciplina">Disciplina</option>
                                <option value="Operativa">Operativa</option>
                                <option value="Administrativa">Administrativa</option>
                                <option value="Penal">Penal Militar</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Fecha de Emisión</label>
                            <input type="date" id="lawDate" required>
                        </div>
                    </div>
                </form>
            </div>
            <div class="modal-footer">
                <button class="btn-secondary" onclick="closeModal('lawModal')">Cancelar</button>
                <button class="btn-primary" onclick="saveLaw()">Guardar</button>
            </div>
        </div>
    </div>

    <!-- Announcement Modal -->
    <div class="modal" id="announcementModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="announcementModalTitle">Nuevo Anuncio</h2>
                <button class="close-btn" onclick="closeModal('announcementModal')">&times;</button>
            </div>
            <div class="modal-body">
                <form id="announcementForm">
                    <input type="hidden" id="announcementId">
                    <div class="form-group">
                        <label>Título</label>
                        <input type="text" id="announcementTitle" required>
                    </div>
                    <div class="form-group">
                        <label>Contenido</label>
                        <textarea id="announcementContent" rows="5" required></textarea>
                    </div>
                    <div class="form-row">
                        <div class="form-group">
                            <label>Prioridad</label>
                            <select id="announcementPriority">
                                <option value="high">Alta</option>
                                <option value="medium" selected>Media</option>
                                <option value="low">Baja</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label>Fecha</label>
                            <input type="date" id="announcementDate" required>
                        </div>
                    </div>
                </form>
            </div>
            <div class="modal-footer">
                <button class="btn-secondary" onclick="closeModal('announcementModal')">Cancelar</button>
                <button class="btn-primary" onclick="saveAnnouncement()">Publicar</button>
            </div>
        </div>
    </div>

    <!-- Toast Container -->
    <div class="toast-container" id="toastContainer"></div>

    <script>
        // Data Storage
        let members = JSON.parse(localStorage.getItem('ea_members')) || [
            { id: 1, name: "Juan Martínez", rank: "General de Brigada", unit: "Comando General", specialty: "Estrategia", date: "2020-01-15", status: "Activo" },
            { id: 2, name: "María González", rank: "Coronel", unit: "I Brigada", specialty: "Inteligencia", date: "2018-03-22", status: "Activo" },
            { id: 3, name: "Carlos Rodríguez", rank: "Mayor", unit: "II Brigada", specialty: "Caballería", date: "2019-07-10", status: "Activo" },
            { id: 4, name: "Ana López", rank: "Capitán", unit: "Fuerza Aérea", specialty: "Piloto", date: "2021-11-05", status: "Licencia" }
        ];

        let ranks = JSON.parse(localStorage.getItem('ea_ranks')) || [
            { id: 1, name: "Soldado", level: 1, description: "Personal de tropa inicial", insignia: "⚪" },
            { id: 2, name: "Cabo", level: 2, description: "Liderazgo de escuadra", insignia: "⚫" },
            { id: 3, name: "Sargento", level: 3, description: "Mando de sección", insignia: "🥉" },
            { id: 4, name: "Suboficial", level: 4, description: "Personal de suboficiales", insignia: "🥈" },
            { id: 5, name: "Oficial Subalterno", level: 5, description: "Oficiales junior", insignia: "⭐" },
            { id: 6, name: "Oficial Superior", level: 6, description: "Mando de compañía", insignia: "⭐⭐" },
            { id: 7, name: "Coronel", level: 7, description: "Mando de regimiento", insignia: "🦅" },
            { id: 8, name: "General de Brigada", level: 8, description: "Mando de brigada", insignia: "🎖️" },
            { id: 9, name: "General de División", level: 9, description: "Alto mando", insignia: "🏅" },
            { id: 10, name: "Teniente General", level: 10, description: "Comandante en Jefe", insignia: "⚔️" }
        ];

        let laws = JSON.parse(localStorage.getItem('ea_laws')) || [
            { id: 1, title: "Disciplina y Conducta", content: "Todo personal militar debe mantener conducta ejemplar tanto en servicio como fuera de él. La insubordinación será sancionada severamente.", category: "Disciplina", date: "2023-01-01" },
            { id: 2, title: "Uso de Uniforme", content: "El uniforme reglamentario es obligatorio en todas las instalaciones militares. Debe mantenerse limpio y en perfectas condiciones.", category: "Administrativa", date: "2023-02-15" },
            { id: 3, title: "Protocolo de Armas", content: "El manejo de armas está estrictamente regulado. Solo personal autorizado puede portar armas de fuego.", category: "Operativa", date: "2023-03-10" }
        ];

        let announcements = JSON.parse(localStorage.getItem('ea_announcements')) || [
            { id: 1, title: "Ejercicios de Entrenamiento Primavera", content: "Se informa a todo el personal que del 15 al 30 de noviembre se realizarán ejercicios tácticos en la zona de Campo de Mayo.", priority: "high", date: "2026-02-20" },
            { id: 2, title: "Cambio de Uniforme de Verano", content: "A partir del 1 de diciembre entra en vigencia el uniforme de verano. Consultar regulación A-45.", priority: "medium", date: "2026-02-22" }
        ];

        let currentUser = null;
        let editingId = null;

        // Initialize
        document.addEventListener('DOMContentLoaded', () => {
            updateStats();
            renderMembers();
            renderRanks();
            renderLaws();
            renderAnnouncements();
            populateRankSelect();
        });

        // Login Handler
        document.getElementById('loginForm').addEventListener('submit', (e) => {
            e.preventDefault();
            const username = document.getElementById('username').value;
            const unit = document.getElementById('unit').value;
            
            currentUser = {
                name: username,
                rank: "General de División",
                unit: unit
            };
            
            document.getElementById('userDisplayName').textContent = username;
            document.getElementById('userRank').textContent = unit;
            
            document.getElementById('loginScreen').classList.add('hidden');
            document.getElementById('mainApp').classList.add('active');
            
            showToast(`Bienvenido, ${username}`, 'success');
        });

        function logout() {
            document.getElementById('loginScreen').classList.remove('hidden');
            document.getElementById('mainApp').classList.remove('active');
            document.getElementById('loginForm').reset();
            currentUser = null;
        }

        // Navigation
        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
            document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
            
            document.getElementById(sectionId).classList.add('active');
            event.target.classList.add('active');
            
            updateStats();
        }

        // Modal Functions
        function openModal(modalId) {
            document.getElementById(modalId).classList.add('active');
            editingId = null;
            
            // Reset forms
            const form = document.querySelector(`#${modalId} form`);
            if (form) form.reset();
            
            // Set default dates
            const today = new Date().toISOString().split('T')[0];
            const dateInputs = document.querySelectorAll(`#${modalId} input[type="date"]`);
            dateInputs.forEach(input => input.value = today);
        }

        function closeModal(modalId) {
            document.getElementById(modalId).classList.remove('active');
            editingId = null;
        }

        // Member Functions
        function renderMembers() {
            const tbody = document.getElementById('membersTableBody');
            tbody.innerHTML = '';
            
            members.forEach(member => {
                const row = document.createElement('div');
                row.className = 'table-row';
                row.innerHTML = `
                    <div><span class="rank-badge">${getRankInsignia(member.rank)}</span></div>
                    <div><strong>${member.name}</strong></div>
                    <div>${member.unit}</div>
                    <div>${member.specialty || '-'}</div>
                    <div><span class="status-badge status-${member.status.toLowerCase()}">${member.status}</span></div>
                    <div class="actions">
                        <button class="btn-icon" onclick="editMember(${member.id})" title="Editar">✏️</button>
                        <button class="btn-icon delete" onclick="deleteMember(${member.id})" title="Eliminar">🗑️</button>
                    </div>
                `;
                tbody.appendChild(row);
            });
        }

        function getRankInsignia(rankName) {
            const rank = ranks.find(r => r.name === rankName);
            return rank ? rank.insignia : '⭐';
        }

        function populateRankSelect() {
            const select = document.getElementById('memberRank');
            select.innerHTML = ranks.sort((a, b) => b.level - a.level).map(r => 
                `<option value="${r.name}">${r.name}</option>`
            ).join('');
        }

        function saveMember() {
            const name = document.getElementById('memberName').value;
            const rank = document.getElementById('memberRank').value;
            const unit = document.getElementById('memberUnit').value;
            const specialty = document.getElementById('memberSpecialty').value;
            const date = document.getElementById('memberDate').value;
            const status = document.getElementById('memberStatus').value;
            
            if (!name || !rank || !unit || !date) {
                showToast('Complete todos los campos obligatorios', 'error');
                return;
            }
            
            if (editingId) {
                const index = members.findIndex(m => m.id === editingId);
                members[index] = { ...members[index], name, rank, unit, specialty, date, status };
                showToast('Miembro actualizado correctamente', 'success');
            } else {
                const newId = Math.max(...members.map(m => m.id), 0) + 1;
                members.push({ id: newId, name, rank, unit, specialty, date, status });
                showToast('Miembro agregado correctamente', 'success');
            }
            
            localStorage.setItem('ea_members', JSON.stringify(members));
            closeModal('memberModal');
            renderMembers();
            updateStats();
        }

        function editMember(id) {
            const member = members.find(m => m.id === id);
            if (!member) return;
            
            editingId = id;
            document.getElementById('memberModalTitle').textContent = 'Editar Miembro';
            document.getElementById('memberId').value = id;
            document.getElementById('memberName').value = member.name;
            document.getElementById('memberRank').value = member.rank;
            document.getElementById('memberUnit').value = member.unit;
            document.getElementById('memberSpecialty').value = member.specialty || '';
            document.getElementById('memberDate').value = member.date;
            document.getElementById('memberStatus').value = member.status;
            
            document.getElementById('memberModal').classList.add('active');
        }

        function deleteMember(id) {
            if (!confirm('¿Está seguro de eliminar este miembro?')) return;
            members = members.filter(m => m.id !== id);
            localStorage.setItem('ea_members', JSON.stringify(members));
            renderMembers();
            updateStats();
            showToast('Miembro eliminado', 'success');
        }

        function filterMembers() {
            const search = document.getElementById('searchMembers').value.toLowerCase();
            const rows = document.querySelectorAll('#membersTableBody .table-row');
            
            rows.forEach(row => {
                const text = row.textContent.toLowerCase();
                row.style.display = text.includes(search) ? '' : 'none';
            });
        }

        // Rank Functions
        function renderRanks() {
            const grid = document.getElementById('ranksGrid');
            grid.innerHTML = '';
            
            ranks.sort((a, b) => a.level - b.level).forEach(rank => {
                const card = document.createElement('div');
                card.className = 'rank-card';
                card.innerHTML = `
                    <div class="rank-insignia">${rank.insignia}</div>
                    <div class="rank-name">${rank.name}</div>
                    <div class="rank-level">Nivel ${rank.level}</div>
                    <div class="rank-description">${rank.description}</div>
                    <div style="margin-top: 1rem; display: flex; gap: 0.5rem; justify-content: center;">
                        <button class="btn-icon" onclick="editRank(${rank.id})">✏️</button>
                        <button class="btn-icon delete" onclick="deleteRank(${rank.id})">🗑️</button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        function saveRank() {
            const name = document.getElementById('rankName').value;
            const level = parseInt(document.getElementById('rankLevel').value);
            const description = document.getElementById('rankDescription').value;
            const insignia = document.getElementById('rankInsignia').value || '⭐';
            
            if (!name || !level) {
                showToast('Complete los campos obligatorios', 'error');
                return;
            }
            
            if (editingId) {
                const index = ranks.findIndex(r => r.id === editingId);
                ranks[index] = { ...ranks[index], name, level, description, insignia };
                showToast('Rango actualizado', 'success');
            } else {
                const newId = Math.max(...ranks.map(r => r.id), 0) + 1;
                ranks.push({ id: newId, name, level, description, insignia });
                showToast('Rango agregado', 'success');
            }
            
            localStorage.setItem('ea_ranks', JSON.stringify(ranks));
            closeModal('rankModal');
            renderRanks();
            populateRankSelect();
        }

        function editRank(id) {
            const rank = ranks.find(r => r.id === id);
            if (!rank) return;
            
            editingId = id;
            document.getElementById('rankModalTitle').textContent = 'Editar Rango';
            document.getElementById('rankId').value = id;
            document.getElementById('rankName').value = rank.name;
            document.getElementById('rankLevel').value = rank.level;
            document.getElementById('rankDescription').value = rank.description;
            document.getElementById('rankInsignia').value = rank.insignia;
            
            document.getElementById('rankModal').classList.add('active');
        }

        function deleteRank(id) {
            if (!confirm('¿Eliminar este rango?')) return;
            ranks = ranks.filter(r => r.id !== id);
            localStorage.setItem('ea_ranks', JSON.stringify(ranks));
            renderRanks();
            populateRankSelect();
            showToast('Rango eliminado', 'success');
        }

        // Law Functions
        function renderLaws() {
            const container = document.getElementById('lawsContainer');
            container.innerHTML = '';
            
            laws.forEach((law, index) => {
                const card = document.createElement('div');
                card.className = 'law-card';
                card.innerHTML = `
                    <div class="law-number">${String(index + 1).padStart(2, '0')}</div>
                    <div class="law-title">${law.title}</div>
                    <div class="law-content">${law.content}</div>
                    <div class="law-meta">
                        <span>📁 ${law.category}</span>
                        <span>📅 ${law.date}</span>
                        <span style="margin-left: auto;">
                            <button class="btn-icon" onclick="editLaw(${law.id})">✏️</button>
                            <button class="btn-icon delete" onclick="deleteLaw(${law.id})">🗑️</button>
                        </span>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function saveLaw() {
            const title = document.getElementById('lawTitle').value;
            const content = document.getElementById('lawContent').value;
            const category = document.getElementById('lawCategory').value;
            const date = document.getElementById('lawDate').value;
            
            if (!title || !content || !date) {
                showToast('Complete todos los campos', 'error');
                return;
            }
            
            if (editingId) {
                const index = laws.findIndex(l => l.id === editingId);
                laws[index] = { ...laws[index], title, content, category, date };
                showToast('Ley actualizada', 'success');
            } else {
                const newId = Math.max(...laws.map(l => l.id), 0) + 1;
                laws.push({ id: newId, title, content, category, date });
                showToast('Ley creada', 'success');
            }
            
            localStorage.setItem('ea_laws', JSON.stringify(laws));
            closeModal('lawModal');
            renderLaws();
            updateStats();
        }

        function editLaw(id) {
            const law = laws.find(l => l.id === id);
            if (!law) return;
            
            editingId = id;
            document.getElementById('lawModalTitle').textContent = 'Editar Ley';
            document.getElementById('lawId').value = id;
            document.getElementById('lawTitle').value = law.title;
            document.getElementById('lawContent').value = law.content;
            document.getElementById('lawCategory').value = law.category;
            document.getElementById('lawDate').value = law.date;
            
            document.getElementById('lawModal').classList.add('active');
        }

        function deleteLaw(id) {
            if (!confirm('¿Eliminar esta ley?')) return;
            laws = laws.filter(l => l.id !== id);
            localStorage.setItem('ea_laws', JSON.stringify(laws));
            renderLaws();
            updateStats();
            showToast('Ley eliminada', 'success');
        }

        // Announcement Functions
        function renderAnnouncements() {
            const container = document.getElementById('announcementsContainer');
            container.innerHTML = '';
            
            announcements.sort((a, b) => new Date(b.date) - new Date(a.date)).forEach(ann => {
                const card = document.createElement('div');
                card.className = 'announcement-card';
                card.innerHTML = `
                    <div class="announcement-header">
                        <div>
                            <div class="announcement-title">${ann.title}</div>
                            <div class="announcement-date">${ann.date}</div>
                        </div>
                        <span class="announcement-priority priority-${ann.priority}">${ann.priority}</span>
                    </div>
                    <div class="announcement-content">${ann.content}</div>
                    <div style="margin-top: 1rem; text-align: right;">
                        <button class="btn-icon" onclick="editAnnouncement(${ann.id})">✏️</button>
                        <button class="btn-icon delete" onclick="deleteAnnouncement(${ann.id})">🗑️</button>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function saveAnnouncement() {
            const title = document.getElementById('announcementTitle').value;
            const content = document.getElementById('announcementContent').value;
            const priority = document.getElementById('announcementPriority').value;
            const date = document.getElementById('announcementDate').value;
            
            if (!title || !content || !date) {
                showToast('Complete todos los campos', 'error');
                return;
            }
            
            if (editingId) {
                const index = announcements.findIndex(a => a.id === editingId);
                announcements[index] = { ...announcements[index], title, content, priority, date };
                showToast('Anuncio actualizado', 'success');
            } else {
                const newId = Math.max(...announcements.map(a => a.id), 0) + 1;
                announcements.push({ id: newId, title, content, priority, date });
                showToast('Anuncio publicado', 'success');
            }
            
            localStorage.setItem('ea_announcements', JSON.stringify(announcements));
            closeModal('announcementModal');
            renderAnnouncements();
            updateStats();
        }

        function editAnnouncement(id) {
            const ann = announcements.find(a => a.id === id);
            if (!ann) return;
            
            editingId = id;
            document.getElementById('announcementModalTitle').textContent = 'Editar Anuncio';
            document.getElementById('announcementId').value = id;
            document.getElementById('announcementTitle').value = ann.title;
            document.getElementById('announcementContent').value = ann.content;
            document.getElementById('announcementPriority').value = ann.priority;
            document.getElementById('announcementDate').value = ann.date;
            
            document.getElementById('announcementModal').classList.add('active');
        }

        function deleteAnnouncement(id) {
            if (!confirm('¿Eliminar este anuncio?')) return;
            announcements = announcements.filter(a => a.id !== id);
            localStorage.setItem('ea_announcements', JSON.stringify(announcements));
            renderAnnouncements();
            updateStats();
            showToast('Anuncio eliminado', 'success');
        }

        // Utilities
        function updateStats() {
            document.getElementById('totalMembers').textContent = members.length;
            document.getElementById('totalLaws').textContent = laws.length;
            document.getElementById('pendingAnnouncements').textContent = 
                announcements.filter(a => a.priority === 'high').length;
        }

        function refreshData() {
            renderMembers();
            renderRanks();
            renderLaws();
            renderAnnouncements();
            updateStats();
            showToast('Datos actualizados', 'success');
        }

        function showToast(message, type = 'success') {
            const container = document.getElementById('toastContainer');
            const toast = document.createElement('div');
            toast.className = `toast ${type}`;
            toast.textContent = message;
            container.appendChild(toast);
            
            setTimeout(() => {
                toast.remove();
            }, 3000);
        }

        // Close modals on outside click
        window.onclick = function(event) {
            if (event.target.classList.contains('modal')) {
                event.target.classList.remove('active');
                editingId = null;
            }
        }
    </script>
</body>
</html>
