<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Henhenbak AI - Siêu Trợ Lý Trí Tuệ Nhân Tạo</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            -webkit-tap-highlight-color: transparent;
        }
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(148, 163, 184, 0.4);
            border-radius: 9999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: rgba(99, 102, 241, 0.6);
        }
        .code-block-wrapper pre {
            overflow-x: auto;
            padding: 1rem;
            border-radius: 0.75rem;
            background-color: #0f172a;
            color: #f8fafc;
            font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;
            font-size: 0.82rem;
            line-height: 1.5;
        }
    </style>
</head>
<body class="bg-slate-100 dark:bg-slate-950 text-slate-900 dark:text-slate-100 h-[100dvh] overflow-hidden select-none">

    <!-- AUTH CONTAINER (GIAO DIỆN ĐĂNG NHẬP GỐC) -->
    <div id="auth-container" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/60 backdrop-blur-sm p-4 overflow-y-auto">
        <div class="bg-white dark:bg-slate-900 rounded-3xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-md p-7 sm:p-8 relative my-auto">
            <div class="text-center mb-6">
                <div class="w-14 h-14 rounded-2xl bg-indigo-600 text-white flex items-center justify-center text-2xl font-extrabold mx-auto mb-4 shadow-lg shadow-indigo-500/30">H</div>
                <h1 class="text-2xl font-extrabold text-slate-900 dark:text-white leading-tight" id="auth-title">Đăng nhập Henhenbak AI</h1>
                <p class="text-xs sm:text-sm text-slate-500 dark:text-slate-400 mt-1.5" id="auth-subtitle">Trợ lý AI thông minh đỉnh cao - Đồng bộ đa thiết bị</p>
            </div>

            <div id="auth-error" class="mb-4 p-3 rounded-xl bg-rose-500/10 border border-rose-500/20 text-rose-600 dark:text-rose-400 text-xs font-semibold hidden text-center"></div>

            <form id="auth-form" onsubmit="handleAuthSubmit(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">TÊN TÀI KHOẢN</label>
                    <div class="relative">
                        <i class="fa-solid fa-user absolute left-4 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
                        <input type="text" id="auth-username" required autocapitalize="none" autocorrect="off" spellcheck="false" placeholder="Nhập tên tài khoản" class="w-full pl-11 pr-4 py-3 rounded-xl border border-slate-300 dark:border-slate-700 bg-slate-50 dark:bg-slate-800/80 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 transition">
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-bold uppercase tracking-wider text-slate-500 dark:text-slate-400 mb-1.5">MẬT KHẨU</label>
                    <div class="relative">
                        <i class="fa-solid fa-lock absolute left-4 top-1/2 -translate-y-1/2 text-slate-400 text-sm"></i>
                        <input type="password" id="auth-password" required placeholder="••••••••" class="w-full pl-11 pr-11 py-3 rounded-xl border border-slate-300 dark:border-slate-700 bg-slate-50 dark:bg-slate-800/80 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 transition">
                        <button type="button" onclick="togglePasswordVisibility()" class="absolute right-3.5 top-1/2 -translate-y-1/2 text-slate-400 hover:text-slate-600 dark:hover:text-slate-200 p-1">
                            <i class="fa-solid fa-eye text-sm" id="auth-eye-icon"></i>
                        </button>
                    </div>
                </div>

                <!-- Công tắc Bật/Tắt Lưu Tài Khoản -->
                <div class="flex items-center justify-between pt-1 pb-1 px-1">
                    <span class="text-xs font-semibold text-slate-600 dark:text-slate-300 flex items-center gap-2">
                        <i class="fa-solid fa-shield-heart text-indigo-500"></i> Lưu tài khoản & mật khẩu
                    </span>
                    <label class="relative inline-flex items-center cursor-pointer">
                        <input type="checkbox" id="remember-account-toggle" class="sr-only peer" checked onchange="handleRememberToggleChange()">
                        <div class="w-11 h-6 bg-slate-300 peer-focus:outline-none rounded-full peer dark:bg-slate-700 peer-checked:after:translate-x-full peer-checked:after:border-white after:content-[''] after:absolute after:top-[2px] after:left-[2px] after:bg-white after:border-slate-300 after:border after:rounded-full after:h-5 after:w-5 after:transition-all peer-checked:bg-indigo-600"></div>
                    </label>
                </div>

                <div class="pt-1">
                    <button type="submit" id="auth-submit-btn" class="w-full py-3.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 active:scale-[0.99] text-white font-bold text-sm shadow-lg shadow-indigo-500/30 transition">
                        Đăng Nhập
                    </button>
                </div>
            </form>

            <div class="mt-4 pt-3 border-t border-slate-200 dark:border-slate-800 text-center">
                <button type="button" onclick="openSyncModal()" class="w-full py-2.5 px-3 rounded-xl bg-emerald-500/10 hover:bg-emerald-500/20 text-emerald-600 dark:text-emerald-400 border border-emerald-500/20 font-bold text-xs flex items-center justify-center gap-1.5 transition">
                    <i class="fa-solid fa-rotate"></i> Đồng Bộ Data Từ Máy Khác (Mã 10 Kí Tự)
                </button>
            </div>
        </div>
    </div>

    <!-- MAIN APP CONTAINER -->
    <div id="main-app" class="h-[100dvh] w-screen flex overflow-hidden hidden">
        <!-- Mobile Sidebar Backdrop -->
        <div id="sidebar-backdrop" onclick="toggleSidebar()" class="fixed inset-0 z-30 bg-slate-900/50 backdrop-blur-xs hidden md:hidden"></div>

        <!-- SIDEBAR -->
        <aside id="sidebar" class="fixed md:static inset-y-0 left-0 z-40 w-72 bg-white dark:bg-slate-900 border-r border-slate-200 dark:border-slate-800 flex flex-col transform -translate-x-full md:translate-x-0 transition-transform duration-300">
            <!-- Brand Header -->
            <div class="p-4 border-b border-slate-200 dark:border-slate-800 flex items-center justify-between">
                <div class="flex items-center space-x-3">
                    <div class="w-9 h-9 rounded-xl bg-indigo-600 text-white flex items-center justify-center font-extrabold text-lg shadow-md shadow-indigo-500/20">H</div>
                    <div>
                        <div class="font-bold text-sm text-slate-900 dark:text-white flex items-center gap-1.5">
                            Henhenbak AI
                            <span class="px-1.5 py-0.5 text-[10px] rounded-md bg-indigo-500/10 text-indigo-600 dark:text-indigo-400 font-extrabold">PRO</span>
                        </div>
                        <div class="text-[11px] text-emerald-500 font-semibold flex items-center gap-1">
                            <span class="w-1.5 h-1.5 rounded-full bg-emerald-500 animate-pulse"></span> Đang hoạt động
                        </div>
                    </div>
                </div>
                <button onclick="toggleSidebar()" class="md:hidden p-2 rounded-lg text-slate-400 hover:bg-slate-100 dark:hover:bg-slate-800">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <!-- Wallet & Utilities Box -->
            <div class="p-3.5 m-3 rounded-2xl bg-slate-50 dark:bg-slate-800/60 border border-slate-200/80 dark:border-slate-800 space-y-2.5">
                <div class="flex items-center justify-between">
                    <span class="text-xs font-semibold text-slate-500 dark:text-slate-400">Số dư:</span>
                    <span class="text-sm font-extrabold text-indigo-600 dark:text-indigo-400" id="user-balance-display">0 đ</span>
                </div>
                <div class="grid grid-cols-2 gap-1.5">
                    <button onclick="openVipModal()" class="py-2 px-2.5 rounded-xl bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-600 hover:to-orange-600 text-white font-bold text-xs shadow-sm flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-crown"></i> Mua VIP
                    </button>
                    <button onclick="openRedeemModal()" class="py-2 px-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs shadow-sm flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-ticket"></i> Nhập Code
                    </button>
                    <button onclick="openInventoryModal()" class="py-2 px-2.5 rounded-xl bg-white dark:bg-slate-800 hover:bg-slate-100 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700 font-bold text-xs flex items-center justify-center gap-1.5 relative">
                        <i class="fa-solid fa-box-open text-indigo-500"></i> Túi Đồ
                        <span id="inventory-count-badge" class="hidden px-1.5 py-0.2 rounded-full bg-rose-500 text-white text-[10px] font-extrabold">0</span>
                    </button>
                    <button onclick="openSyncModal()" class="py-2 px-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white font-bold text-xs shadow-sm flex items-center justify-center gap-1.5">
                        <i class="fa-solid fa-rotate"></i> Đồng Bộ PC/Phone
                    </button>
                </div>
            </div>

            <!-- Admin / VIP Button -->
            <div id="admin-menu-section" class="px-3 mb-2 hidden">
                <button onclick="openAdminModal()" class="w-full py-2.5 px-3 rounded-xl bg-slate-900 dark:bg-indigo-600 hover:opacity-95 text-white font-bold text-xs flex items-center justify-center shadow-md transition">
                    <span><i class="fa-solid fa-shield-halved mr-2"></i> Quản Trị Hệ Thống</span>
                </button>
            </div>

            <!-- New Chat Button -->
            <div class="px-3 mb-2">
                <button onclick="createNewChat()" class="w-full py-2.5 px-3 rounded-xl border border-dashed border-indigo-400 dark:border-indigo-500/60 text-indigo-600 dark:text-indigo-400 hover:bg-indigo-50 dark:hover:bg-indigo-950/30 font-bold text-xs flex items-center justify-center gap-2 transition">
                    <i class="fa-solid fa-plus"></i> Cuộc trò chuyện mới
                </button>
            </div>

            <!-- Chat History List -->
            <div class="px-3 py-1 text-[11px] font-bold uppercase tracking-wider text-slate-400">Lịch sử trò chuyện</div>
            <div id="chat-history-list" class="flex-1 overflow-y-auto px-3 space-y-1 py-1"></div>

            <!-- User Info Footer -->
            <div class="p-4 border-t border-slate-200 dark:border-slate-800 flex items-center justify-between bg-slate-50/50 dark:bg-slate-900/50">
                <div class="flex items-center space-x-3 overflow-hidden cursor-pointer" onclick="openProfileModal(currentUser.username)">
                    <div class="w-9 h-9 rounded-full bg-gradient-to-tr from-indigo-500 to-purple-500 text-white flex items-center justify-center font-bold text-sm flex-shrink-0 overflow-hidden bg-cover bg-center" id="user-avatar-initial">H</div>
                    <div class="truncate">
                        <div class="font-semibold text-sm truncate text-slate-900 dark:text-white" id="user-display-name">henhenbak</div>
                        <div class="text-xs text-indigo-600 dark:text-indigo-400 font-bold truncate" id="user-role-badge">admin web</div>
                    </div>
                </div>
                <div class="flex items-center space-x-1">
                    <button onclick="toggleTheme()" title="Đổi giao diện Sáng/Tối" class="p-2 rounded-lg text-slate-500 hover:bg-slate-200/70 dark:hover:bg-slate-800 transition">
                        <i class="fa-solid fa-moon dark:hidden"></i>
                        <i class="fa-solid fa-sun hidden dark:inline text-amber-400"></i>
                    </button>
                    <button onclick="handleLogout()" title="Đăng xuất" class="p-2 rounded-lg text-rose-500 hover:bg-rose-500/10 transition">
                        <i class="fa-solid fa-right-from-bracket"></i>
                    </button>
                </div>
            </div>
        </aside>

        <!-- MAIN CHAT CONTENT -->
        <main class="flex-1 flex flex-col bg-slate-50 dark:bg-slate-950 h-full overflow-hidden relative">
            <!-- Header -->
            <header class="h-14 px-3 sm:px-6 bg-white/80 dark:bg-slate-900/80 backdrop-blur-md border-b border-slate-200 dark:border-slate-800 flex items-center justify-between flex-shrink-0 z-10">
                <div class="flex items-center space-x-2.5 overflow-hidden">
                    <button onclick="toggleSidebar()" class="md:hidden p-2 rounded-xl bg-slate-100 dark:bg-slate-800 text-slate-600 dark:text-slate-300">
                        <i class="fa-solid fa-bars"></i>
                    </button>
                    <div class="truncate">
                        <h2 class="font-bold text-xs sm:text-base text-slate-900 dark:text-white truncate" id="current-chat-title">Trợ lý thông minh Henhenbak AI</h2>
                        <p class="text-[10px] sm:text-[11px] text-slate-500 dark:text-slate-400 truncate">Tích hợp Gemini 3 Flash • GPT-4o • Giải đáp mọi môn học & Viết Code</p>
                    </div>
                </div>
                <div class="flex items-center gap-1.5 flex-shrink-0">
                    <button onclick="openVipModal()" class="px-2.5 py-1.5 rounded-xl bg-gradient-to-r from-amber-500 to-orange-500 text-white text-xs font-bold flex items-center gap-1.5 shadow-sm hover:opacity-95 transition">
                        <i class="fa-solid fa-crown"></i> <span class="hidden sm:inline">VIP Premium</span>
                    </button>
                    <button onclick="openSyncModal()" class="px-2.5 py-1.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-xs font-bold flex items-center gap-1.5 shadow-sm transition">
                        <i class="fa-solid fa-rotate"></i> <span class="hidden sm:inline">Đồng Bộ 10 Kí Tự</span>
                    </button>
                </div>
            </header>

            <!-- Messages List -->
            <div id="chat-messages" class="flex-1 overflow-y-auto p-3 sm:p-5 space-y-4"></div>

            <!-- Chat Input Footer -->
            <div class="p-2.5 sm:p-3.5 bg-white dark:bg-slate-900 border-t border-slate-200 dark:border-slate-800 flex-shrink-0">
                <div class="max-w-4xl mx-auto">
                    <div id="attachment-preview" class="hidden mb-2 px-3 py-1.5 rounded-xl bg-indigo-50 dark:bg-slate-800 border border-indigo-200 dark:border-slate-700 flex items-center justify-between text-xs">
                        <div class="flex items-center gap-2 truncate">
                            <i class="fa-solid fa-image text-indigo-600"></i>
                            <span id="attachment-name" class="font-semibold truncate text-slate-700 dark:text-slate-200">file.png</span>
                        </div>
                        <button type="button" onclick="removeAttachedFile()" class="text-rose-500 hover:text-rose-700 font-bold ml-2">
                            <i class="fa-solid fa-xmark"></i>
                        </button>
                    </div>
                    <div class="flex items-end gap-2 bg-slate-100 dark:bg-slate-800/90 p-1.5 sm:p-2 rounded-2xl border border-slate-200 dark:border-slate-700/80 focus-within:ring-2 focus-within:ring-indigo-500 transition">
                        <button type="button" onclick="triggerFileInput()" title="Đính kèm ảnh hoặc file" class="w-9 h-9 sm:w-10 sm:h-10 rounded-xl text-slate-500 hover:text-indigo-600 hover:bg-white dark:hover:bg-slate-700 flex items-center justify-center flex-shrink-0 transition">
                            <i class="fa-solid fa-paperclip"></i>
                        </button>
                        <input type="file" id="file-input" onchange="handleFileSelected(event)" class="hidden" accept="image/*,.txt,.lua,.py,.js,.html,.json">
                        <textarea id="chat-input" rows="1" placeholder="Nhập câu hỏi, bài tập hoặc yêu cầu viết code..." onkeydown="handleChatKeyDown(event)" oninput="this.style.height='auto';this.style.height=Math.min(this.scrollHeight,120)+'px'" class="flex-1 bg-transparent border-0 focus:ring-0 focus:outline-none text-xs sm:text-sm text-slate-900 dark:text-white py-2 px-1 resize-none max-h-32 select-text"></textarea>
                        <button type="button" id="send-btn" onclick="sendMessage()" class="w-9 h-9 sm:w-10 sm:h-10 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white flex items-center justify-center flex-shrink-0 shadow-md shadow-indigo-500/20 transition">
                            <i class="fa-solid fa-paper-plane text-xs"></i>
                        </button>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- SYNC MODAL (Mã 10 Kí Tự Siêu Ngắn) -->
    <div id="sync-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3 sm:p-4">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-md p-4 sm:p-5 relative flex flex-col text-slate-900 dark:text-slate-100 space-y-3 max-h-[88vh] overflow-y-auto">
            <div class="flex items-center justify-between pb-2.5 border-b border-slate-200 dark:border-slate-800 flex-shrink-0">
                <h3 class="font-bold text-sm sm:text-base flex items-center gap-2"><i class="fa-solid fa-cloud-arrow-up text-indigo-500"></i> Đồng Bộ PC & Điện Thoại (10 Kí Tự)</h3>
                <button type="button" onclick="closeSyncModal()" title="Thoát" class="w-8 h-8 rounded-full bg-slate-100 dark:bg-slate-800 hover:bg-rose-500 hover:text-white text-slate-600 dark:text-slate-300 flex items-center justify-center transition flex-shrink-0">
                    <i class="fa-solid fa-xmark text-sm"></i>
                </button>
            </div>
            <div class="text-[11px] sm:text-xs text-slate-500 leading-relaxed">
                Tạo mã <b>10 kí tự</b> trên máy này rồi nhập sang máy khác và bấm <b>Kích Hoạt</b> để đồng bộ 100% tài khoản, số dư, VIP và lịch sử chat.
            </div>
            <div>
                <div class="flex items-center justify-between mb-1">
                    <label class="block text-[11px] font-semibold uppercase text-slate-500">Mã Sync 10 Kí Tự (Cloud)</label>
                    <span id="sync-copy-status" class="text-[11px] font-bold text-emerald-500 hidden">Đã sao chép!</span>
                </div>
                <input type="text" id="sync-data-textarea" maxlength="10" placeholder="Nhập mã 10 kí tự..." class="w-full px-3 py-2.5 rounded-xl border border-slate-300 dark:border-slate-700 bg-slate-50 dark:bg-slate-800 text-sm sm:text-base font-mono text-indigo-600 dark:text-indigo-400 font-extrabold text-center tracking-widest uppercase select-all">
            </div>
            <div class="grid grid-cols-3 gap-2 pt-1">
                <button type="button" id="btn-export-sync" onclick="exportSyncData()" class="py-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-semibold text-xs shadow-sm flex items-center justify-center gap-1"><i class="fa-solid fa-key"></i> Tạo Mã</button>
                <button type="button" onclick="copySyncData()" class="py-2.5 rounded-xl bg-amber-500 hover:bg-amber-600 text-white font-semibold text-xs shadow-sm flex items-center justify-center gap-1"><i class="fa-regular fa-copy"></i> Sao Chép</button>
                <button type="button" id="btn-import-sync" onclick="importSyncData()" class="py-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white font-semibold text-xs shadow-sm flex items-center justify-center gap-1"><i class="fa-solid fa-bolt"></i> Kích Hoạt</button>
            </div>
        </div>
    </div>

    <!-- PROFILE MODAL (HỒ SƠ) -->
    <div id="profile-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3 sm:p-4">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-sm overflow-hidden relative text-slate-900 dark:text-slate-100 max-h-[88vh] overflow-y-auto">
            <div id="profile-bg-preview" class="h-24 bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 bg-cover bg-center relative">
                <button type="button" onclick="closeProfileModal()" title="Thoát" class="absolute top-2.5 right-2.5 w-8 h-8 rounded-full bg-slate-900/70 hover:bg-rose-600 text-white flex items-center justify-center shadow-md transition">
                    <i class="fa-solid fa-xmark text-sm"></i>
                </button>
            </div>
            <div class="px-4 pb-4 pt-0 relative">
                <div class="flex justify-between items-end -mt-8 mb-3">
                    <div class="relative group">
                        <div class="w-16 h-16 rounded-2xl border-4 border-white dark:border-slate-900 bg-gradient-to-tr from-indigo-600 to-purple-600 text-white flex items-center justify-center text-2xl font-bold shadow-md overflow-hidden bg-cover bg-center" id="profile-avatar-char">U</div>
                        <button type="button" id="profile-avatar-upload-btn" onclick="triggerAvatarFileInput()" title="Tải ảnh đại diện từ máy" class="absolute -bottom-1 -right-1 w-6 h-6 rounded-lg bg-indigo-600 hover:bg-indigo-700 text-white flex items-center justify-center shadow-md border-2 border-white dark:border-slate-900">
                            <i class="fa-solid fa-camera text-[10px]"></i>
                        </button>
                        <input type="file" id="avatar-file-input" onchange="handleAvatarFileSelected(event)" class="hidden" accept="image/*">
                    </div>
                    <button type="button" id="profile-bg-upload-btn" onclick="triggerBgFileInput()" class="px-2.5 py-1.5 rounded-xl bg-slate-100 dark:bg-slate-800 hover:bg-indigo-50 dark:hover:bg-slate-700 text-indigo-600 dark:text-indigo-400 text-[11px] font-bold border border-slate-200 dark:border-slate-700 flex items-center gap-1 shadow-xs">
                        <i class="fa-solid fa-image"></i> Đổi ảnh bìa
                    </button>
                    <input type="file" id="bg-file-input" onchange="handleBgFileSelected(event)" class="hidden" accept="image/*">
                </div>
                <div class="space-y-2.5">
                    <div>
                        <h3 class="text-base font-extrabold flex items-center gap-2" id="profile-username">username</h3>
                        <div class="text-[11px] text-indigo-600 dark:text-indigo-400 font-bold uppercase tracking-wider" id="profile-role">member</div>
                    </div>
                    <div class="grid grid-cols-2 gap-2 py-2 border-y border-slate-200 dark:border-slate-800 text-xs">
                        <div><span class="text-slate-400">Số dư:</span> <span class="font-extrabold text-slate-900 dark:text-white" id="profile-balance">0 đ</span></div>
                        <div><span class="text-slate-400">Gói VIP:</span> <span class="font-extrabold text-amber-500" id="profile-vip-status">Không có</span></div>
                    </div>
                    <div id="profile-vip-expiration-box" class="p-2 rounded-xl bg-amber-500/10 border border-amber-500/20 text-[11px] text-amber-700 dark:text-amber-300 font-semibold hidden">
                        <i class="fa-solid fa-clock mr-1"></i> Hết hạn: <span id="profile-expiration-time">--</span>
                    </div>
                    <div id="profile-customize-section" class="pt-1 space-y-2">
                        <div class="grid grid-cols-2 gap-2">
                            <button type="button" onclick="triggerAvatarFileInput()" class="py-2 px-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white text-[11px] font-bold flex items-center justify-center gap-1 shadow-xs">
                                <i class="fa-solid fa-paperclip"></i> Ảnh Đại Diện
                            </button>
                            <button type="button" onclick="triggerBgFileInput()" class="py-2 px-2.5 rounded-xl bg-purple-600 hover:bg-purple-700 text-white text-[11px] font-bold flex items-center justify-center gap-1 shadow-xs">
                                <i class="fa-solid fa-paperclip"></i> Ảnh Bìa
                            </button>
                        </div>
                        <div id="profile-upload-status" class="text-[11px] text-emerald-500 font-bold text-center hidden">Đã cập nhật ảnh hồ sơ!</div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- VIP SHOP MODAL -->
    <div id="vip-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3 sm:p-4">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-md p-4 relative text-slate-900 dark:text-slate-100 max-h-[88vh] flex flex-col">
            <div class="flex items-center justify-between pb-2.5 border-b border-slate-200 dark:border-slate-800 flex-shrink-0">
                <div class="pr-2">
                    <h3 class="font-extrabold text-sm sm:text-base flex items-center gap-1.5">
                        <i class="fa-solid fa-crown text-amber-500"></i> Nâng Cấp VIP (Premium)
                    </h3>
                    <p class="text-[11px] text-slate-500">Mở khóa đặc quyền VIP & tính năng cao cấp</p>
                </div>
                <button type="button" onclick="closeVipModal()" title="Đóng / Thoát" class="w-8 h-8 rounded-full bg-slate-100 dark:bg-slate-800 hover:bg-rose-500 hover:text-white text-slate-600 dark:text-slate-300 flex items-center justify-center transition flex-shrink-0">
                    <i class="fa-solid fa-xmark text-base"></i>
                </button>
            </div>

            <div id="vip-buy-message" class="mt-2.5 p-2.5 rounded-xl text-xs font-bold hidden flex-shrink-0"></div>

            <div class="space-y-2 my-2.5 overflow-y-auto pr-0.5">
                <!-- VIP 1 Ngày -->
                <div class="p-2.5 rounded-xl border border-slate-200 dark:border-slate-800 bg-slate-50 dark:bg-slate-800/50 flex items-center justify-between gap-2.5">
                    <div class="min-w-0">
                        <div class="flex items-center gap-1.5">
                            <span class="font-extrabold text-xs sm:text-sm">VIP 1 Ngày</span>
                            <span class="text-[9px] font-bold uppercase px-1.5 py-0.5 rounded bg-amber-500/15 text-amber-600 dark:text-amber-400">Trải nghiệm</span>
                        </div>
                        <div class="text-xs sm:text-sm font-black text-indigo-600 dark:text-indigo-400">20,000 đ</div>
                        <p class="text-[10px] text-slate-500 truncate">Sử dụng toàn bộ tính năng VIP trong 24 giờ.</p>
                    </div>
                    <button type="button" onclick="selectVipPackage('1d', 20000, 'Gói VIP 1 Ngày')" class="px-3 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs shadow-sm flex-shrink-0 transition">
                        Nâng Cấp
                    </button>
                </div>

                <!-- VIP 1 Tháng (250,000 đ) -->
                <div class="p-2.5 rounded-xl border-2 border-indigo-500 bg-indigo-50/30 dark:bg-indigo-950/20 flex items-center justify-between gap-2.5">
                    <div class="min-w-0">
                        <div class="flex items-center gap-1.5">
                            <span class="font-extrabold text-xs sm:text-sm">VIP 1 Tháng</span>
                            <span class="text-[9px] font-bold uppercase px-1.5 py-0.5 rounded bg-indigo-600 text-white">Phổ biến</span>
                        </div>
                        <div class="text-xs sm:text-sm font-black text-indigo-600 dark:text-indigo-400">250,000 đ</div>
                        <p class="text-[10px] text-slate-500 truncate">Sử dụng toàn bộ tính năng VIP trong 30 ngày.</p>
                    </div>
                    <button type="button" onclick="selectVipPackage('30d', 250000, 'Gói VIP 1 Tháng')" class="px-3 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs shadow-sm flex-shrink-0 transition">
                        Nâng Cấp
                    </button>
                </div>

                <!-- VIP 1 Năm -->
                <div class="p-2.5 rounded-xl border border-slate-200 dark:border-slate-800 bg-slate-50 dark:bg-slate-800/50 flex items-center justify-between gap-2.5">
                    <div class="min-w-0">
                        <div class="flex items-center gap-1.5">
                            <span class="font-extrabold text-xs sm:text-sm">VIP 1 Năm</span>
                            <span class="text-[9px] font-bold uppercase px-1.5 py-0.5 rounded bg-purple-500/15 text-purple-600 dark:text-purple-400">Siêu cấp</span>
                        </div>
                        <div class="text-xs sm:text-sm font-black text-indigo-600 dark:text-indigo-400">999,000 đ</div>
                        <p class="text-[10px] text-slate-500 truncate">Đặc quyền VIP 365 ngày siêu tiết kiệm.</p>
                    </div>
                    <button type="button" onclick="selectVipPackage('365d', 999000, 'Gói VIP 1 Năm')" class="px-3 py-2 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs shadow-sm flex-shrink-0 transition">
                        Nâng Cấp
                    </button>
                </div>

                <!-- VIP Vĩnh Viễn (10,000,000 đ) -->
                <div class="p-2.5 rounded-xl border-2 border-amber-500 bg-gradient-to-r from-amber-500/10 to-orange-500/10 flex items-center justify-between gap-2.5">
                    <div class="min-w-0">
                        <div class="flex items-center gap-1.5">
                            <span class="font-extrabold text-xs sm:text-sm text-amber-600 dark:text-amber-400">VIP Vĩnh Viễn</span>
                            <span class="text-[9px] font-bold uppercase px-1.5 py-0.5 rounded bg-gradient-to-r from-amber-500 to-orange-500 text-white">Tối Thượng</span>
                        </div>
                        <div class="text-xs sm:text-sm font-black text-amber-600 dark:text-amber-400">10,000,000 đ</div>
                        <p class="text-[10px] text-slate-500 truncate">Sở hữu đặc quyền VIP trọn đời không giới hạn.</p>
                    </div>
                    <button type="button" onclick="selectVipPackage('perm', 10000000, 'Gói VIP Vĩnh Viễn')" class="px-3 py-2 rounded-xl bg-gradient-to-r from-amber-500 to-orange-500 hover:from-amber-600 hover:to-orange-600 text-white font-bold text-xs shadow-sm flex-shrink-0 transition">
                        Nâng Cấp
                    </button>
                </div>
            </div>

            <div class="pt-2 border-t border-slate-200 dark:border-slate-800 flex justify-end flex-shrink-0">
                <button type="button" onclick="closeVipModal()" class="w-full py-2 rounded-xl bg-slate-200 dark:bg-slate-800 hover:bg-slate-300 dark:hover:bg-slate-700 text-slate-700 dark:text-slate-200 font-bold text-xs transition">
                    <i class="fa-solid fa-xmark mr-1"></i> Đóng / Thoát
                </button>
            </div>
        </div>
    </div>

    <!-- VIP CHOICE MODAL -->
    <div id="vip-choice-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3 sm:p-4">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-xs p-4 relative text-slate-900 dark:text-slate-100 space-y-3">
            <div class="flex items-center justify-between">
                <h3 class="font-extrabold text-sm">Chọn hình thức dùng VIP</h3>
                <button type="button" onclick="closeVipChoiceModal()" class="w-7 h-7 rounded-full bg-slate-100 dark:bg-slate-800 hover:bg-rose-500 hover:text-white text-slate-500 flex items-center justify-center transition"><i class="fa-solid fa-xmark text-xs"></i></button>
            </div>
            <p class="text-xs text-slate-500">Kích hoạt dùng ngay hay cất <b id="vip-choice-pkg-name" class="text-indigo-600">VIP</b> vào Túi đồ?</p>
            <div class="space-y-2">
                <button type="button" onclick="confirmBuyVip('use')" class="w-full py-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs shadow-sm">Kích hoạt dùng ngay</button>
                <button type="button" onclick="confirmBuyVip('bag')" class="w-full py-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white font-bold text-xs shadow-sm">Cất vào Túi đồ</button>
                <button type="button" onclick="closeVipChoiceModal()" class="w-full py-2 rounded-xl bg-slate-200 dark:bg-slate-800 text-slate-700 dark:text-slate-300 font-bold text-xs">Thoát / Hủy</button>
            </div>
        </div>
    </div>

    <!-- REDEEM CODE MODAL -->
    <div id="redeem-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3 sm:p-4">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-sm p-4 relative text-slate-900 dark:text-slate-100 space-y-3">
            <div class="flex items-center justify-between pb-2 border-b border-slate-200 dark:border-slate-800">
                <h3 class="font-extrabold text-sm sm:text-base flex items-center gap-2"><i class="fa-solid fa-ticket text-indigo-500"></i> Nhập Giftcode</h3>
                <button type="button" onclick="closeRedeemModal()" class="w-8 h-8 rounded-full bg-slate-100 dark:bg-slate-800 hover:bg-rose-500 hover:text-white text-slate-500 flex items-center justify-center transition"><i class="fa-solid fa-xmark text-sm"></i></button>
            </div>
            <div id="redeem-status-msg" class="p-2.5 rounded-xl text-xs font-bold hidden"></div>
            <div>
                <label class="block text-[11px] font-bold uppercase text-slate-500 mb-1">Mã Code Quà Tặng</label>
                <input type="text" id="redeem-code-input" placeholder="Nhập mã code tại đây..." class="w-full px-3.5 py-2.5 rounded-xl border border-slate-300 dark:border-slate-700 bg-slate-50 dark:bg-slate-800 text-xs sm:text-sm font-bold uppercase tracking-wider focus:outline-none focus:ring-2 focus:ring-indigo-500">
            </div>
            <div class="flex gap-2">
                <button type="button" onclick="handleRedeemCode()" class="flex-1 py-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs shadow-sm">Xác Nhận</button>
                <button type="button" onclick="closeRedeemModal()" class="px-4 py-2.5 rounded-xl bg-slate-200 dark:bg-slate-800 text-slate-700 dark:text-slate-300 font-bold text-xs">Đóng</button>
            </div>
        </div>
    </div>

    <!-- INVENTORY MODAL -->
    <div id="inventory-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3 sm:p-4">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-sm p-4 relative text-slate-900 dark:text-slate-100 space-y-3">
            <div class="flex items-center justify-between pb-2 border-b border-slate-200 dark:border-slate-800">
                <h3 class="font-extrabold text-sm sm:text-base flex items-center gap-2"><i class="fa-solid fa-box-open text-indigo-500"></i> Túi Đồ Của Bạn</h3>
                <button type="button" onclick="closeInventoryModal()" class="w-8 h-8 rounded-full bg-slate-100 dark:bg-slate-800 hover:bg-rose-500 hover:text-white text-slate-500 flex items-center justify-center transition"><i class="fa-solid fa-xmark text-sm"></i></button>
            </div>
            <div id="inventory-gift-status" class="p-2.5 rounded-xl text-xs font-bold hidden"></div>
            <div id="inventory-list" class="space-y-2 max-h-60 overflow-y-auto"></div>
            <div class="pt-1 border-t border-slate-200 dark:border-slate-800">
                <button type="button" onclick="closeInventoryModal()" class="w-full py-2 rounded-xl bg-slate-200 dark:bg-slate-800 text-slate-700 dark:text-slate-300 font-bold text-xs">Đóng</button>
            </div>
        </div>
    </div>

    <!-- GIFT INPUT MODAL -->
    <div id="gift-input-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3 sm:p-4">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-xs p-4 relative text-slate-900 dark:text-slate-100 space-y-3">
            <div class="flex items-center justify-between pb-2 border-b border-slate-200 dark:border-slate-800">
                <h3 class="font-extrabold text-sm flex items-center gap-1.5">
                    <i class="fa-solid fa-gift text-pink-500"></i> Tặng Quà (Gift VIP)
                </h3>
                <button type="button" onclick="backToInventoryFromGift()" class="w-7 h-7 rounded-full bg-slate-100 dark:bg-slate-800 hover:bg-rose-500 hover:text-white text-slate-500 flex items-center justify-center transition">
                    <i class="fa-solid fa-xmark text-xs"></i>
                </button>
            </div>
            <div class="text-xs text-slate-500">
                Vật phẩm tặng: <b id="gift-item-name-display" class="text-indigo-600 dark:text-indigo-400">Gói VIP</b>
            </div>
            <div id="gift-input-error" class="p-2 rounded-xl bg-rose-500/10 text-rose-500 text-xs font-bold hidden"></div>
            <div>
                <label class="block text-[11px] font-bold uppercase text-slate-500 mb-1">Nhập tên người nhận Gift</label>
                <input type="text" id="gift-recipient-input" placeholder="Nhập tên tài khoản người nhận..." class="w-full px-3 py-2.5 rounded-xl border border-slate-300 dark:border-slate-700 bg-slate-50 dark:bg-slate-800 text-xs font-bold focus:outline-none focus:ring-2 focus:ring-indigo-500">
            </div>
            <div class="grid grid-cols-2 gap-2 pt-1">
                <button type="button" onclick="backToInventoryFromGift()" class="py-2.5 rounded-xl bg-slate-200 dark:bg-slate-800 hover:bg-slate-300 text-slate-700 dark:text-slate-300 font-bold text-xs transition">
                    <i class="fa-solid fa-arrow-left mr-1"></i> Quay lại
                </button>
                <button type="button" onclick="promptGiftConfirmation()" class="py-2.5 rounded-xl bg-gradient-to-r from-pink-500 to-rose-500 hover:from-pink-600 hover:to-rose-600 text-white font-bold text-xs shadow-sm transition">
                    <i class="fa-solid fa-paper-plane mr-1"></i> Gift
                </button>
            </div>
        </div>
    </div>

    <!-- GIFT CONFIRM MODAL -->
    <div id="gift-confirm-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3 sm:p-4">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-xs p-4 relative text-slate-900 dark:text-slate-100 space-y-3 text-center">
            <div class="w-11 h-11 rounded-full bg-pink-500/10 text-pink-500 flex items-center justify-center mx-auto text-lg">
                <i class="fa-solid fa-gift"></i>
            </div>
            <h3 class="font-extrabold text-sm sm:text-base">Bạn chắc chắn chứ?</h3>
            <p class="text-xs text-slate-500 leading-relaxed">
                Bạn có chắc chắn muốn tặng <b id="gift-confirm-item-name" class="text-indigo-600 dark:text-indigo-400">Gói VIP</b> cho tài khoản <b id="gift-confirm-target-user" class="text-pink-600">@user</b> không?
            </p>
            <div class="grid grid-cols-2 gap-2 pt-1">
                <button type="button" onclick="cancelGiftConfirmation()" class="py-2.5 rounded-xl bg-slate-200 dark:bg-slate-800 text-slate-700 dark:text-slate-300 font-bold text-xs">
                    Quay lại
                </button>
                <button type="button" onclick="executeGiftItem()" class="py-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white font-bold text-xs shadow-sm">
                    Chắc chắn
                </button>
            </div>
        </div>
    </div>

    <!-- ADMIN MODAL (BẢNG QUẢN TRỊ HỆ THỐNG) -->
    <div id="admin-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3 sm:p-4 overflow-y-auto">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-xl p-4 sm:p-5 relative text-slate-900 dark:text-slate-100 my-auto max-h-[88vh] flex flex-col">
            <div class="flex items-start justify-between pb-3 border-b border-slate-200 dark:border-slate-800 flex-shrink-0">
                <div class="pr-2">
                    <h3 class="font-extrabold text-base sm:text-lg text-slate-900 dark:text-white" id="admin-modal-title">Bảng Quản Trị Hệ Thống</h3>
                    <p class="text-[11px] text-slate-500 mt-0.5" id="admin-modal-subtitle">Quản lý thành viên, nạp/trừ tiền, cấp/xóa VIP và tạo mã code</p>
                </div>
                <button type="button" onclick="closeAdminModal()" title="Thoát" class="w-8 h-8 rounded-full bg-slate-100 dark:bg-slate-800 hover:bg-rose-500 hover:text-white text-slate-600 dark:text-slate-300 flex items-center justify-center transition flex-shrink-0">
                    <i class="fa-solid fa-xmark text-base"></i>
                </button>
            </div>

            <!-- Navigation Tabs (Role Mod TUYỆT ĐỐI KHÔNG THẤY Tab Cấp Role và Mật Khẩu) -->
            <div id="admin-tabs-bar" class="grid grid-cols-2 sm:grid-cols-4 gap-1.5 my-3 flex-shrink-0">
                <button type="button" id="tab-btn-users" onclick="switchAdminTab('users')" class="py-2 px-2.5 rounded-xl font-bold text-xs bg-indigo-600 text-white shadow-xs transition">
                    Thành Viên
                </button>
                <button type="button" id="tab-btn-codes" onclick="switchAdminTab('codes')" class="py-2 px-2.5 rounded-xl font-bold text-xs bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 transition">
                    Quản Lý Code
                </button>
                <button type="button" id="tab-btn-roles" onclick="switchAdminTab('roles')" class="py-2 px-2.5 rounded-xl font-bold text-xs bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 transition hidden">
                    Cấp & Xóa Role
                </button>
                <button type="button" id="tab-btn-passwords" onclick="switchAdminTab('passwords')" class="py-2 px-2.5 rounded-xl font-bold text-xs bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 transition hidden">
                    Mật Khẩu
                </button>
            </div>

            <div class="flex-1 overflow-y-auto space-y-3 pr-1">
                <!-- TAB 1: QUẢN LÝ THÀNH VIÊN -->
                <div id="admin-tab-users" class="space-y-2.5">
                    <input type="text" id="admin-user-search" oninput="loadNotebookUsers()" placeholder="Tìm kiếm tên tài khoản thành viên..." class="w-full px-3.5 py-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-slate-50 dark:bg-slate-800 text-xs focus:outline-none focus:ring-2 focus:ring-indigo-500">
                    <div id="admin-users-list" class="space-y-2"></div>
                </div>

                <!-- TAB 2: TẠO & QUẢN LÝ CODE -->
                <div id="admin-tab-codes" class="space-y-3 hidden">
                    <div id="vip-weekly-only-box" class="hidden p-4 rounded-2xl bg-amber-500/10 border border-amber-500/30 text-center space-y-2.5">
                        <div class="w-10 h-10 rounded-xl bg-amber-500 text-white flex items-center justify-center mx-auto text-lg shadow-sm">
                            <i class="fa-solid fa-gift"></i>
                        </div>
                        <h4 class="font-extrabold text-sm text-amber-600 dark:text-amber-400">Đặc Quyền Role VIP: Code Premium 1 Ngày Hàng Tuần</h4>
                        <p class="text-[11px] text-slate-500">Mỗi tuần tài khoản Role VIP được nhận miễn phí 1 mã Code VIP 1 Ngày:</p>
                        <div class="p-2.5 rounded-xl bg-white dark:bg-slate-900 border border-amber-400 font-mono font-black text-sm tracking-widest text-indigo-600 dark:text-indigo-400 select-all" id="vip-weekly-code-display">---</div>
                        <button type="button" onclick="copyWeeklyVipCode()" class="px-4 py-2 rounded-xl bg-amber-500 hover:bg-amber-600 text-white font-bold text-xs shadow-sm">
                            <i class="fa-regular fa-copy mr-1"></i> Sao Chép Code Tuần
                        </button>
                    </div>

                    <div id="admin-code-creator-box" class="p-3.5 rounded-2xl bg-slate-50 dark:bg-slate-800/60 border border-slate-200 dark:border-slate-800 space-y-2.5">
                        <div class="text-[11px] font-extrabold uppercase text-indigo-600 dark:text-indigo-400">
                            TẠO MÃ CODE MỚI (ĐỂ TRỐNG SẼ TỰ ĐỘNG SINH MÃ NGẪU NHIÊN 11-19 KÍ TỰ)
                        </div>
                        <input type="text" id="new-code-str" placeholder="VD: VIP1NGAY (để trống tự tạo ngẫu nhiên)" class="w-full px-3.5 py-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 text-xs font-bold uppercase">
                        <div class="grid grid-cols-2 gap-2">
                            <select id="new-code-type" onchange="toggleCodeAmountInput()" class="w-full px-3 py-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 text-xs font-semibold">
                                <option value="money">Code Tiền</option>
                                <option value="vip_1d">Code VIP 1 Ngày</option>
                                <option value="vip_30d">Code VIP 1 Tháng</option>
                                <option value="vip_365d">Code VIP 1 Năm</option>
                                <option value="vip_perm">Code VIP Vĩnh Viễn</option>
                            </select>
                            <select id="new-code-uses" class="w-full px-3 py-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 text-xs font-semibold">
                                <option value="1">1 người</option>
                                <option value="5">5 người</option>
                                <option value="10">10 người</option>
                                <option value="50">50 người</option>
                                <option value="100">100 người</option>
                            </select>
                        </div>
                        <input type="number" id="new-code-amount" value="50000" placeholder="Số tiền thưởng (VD: 50000)" class="w-full px-3.5 py-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 text-xs font-bold">
                        <button type="button" onclick="adminCreateCode()" class="w-full py-2.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs shadow-sm">
                            Tạo Mã Code Ngay
                        </button>
                    </div>

                    <div id="admin-codes-list" class="space-y-2"></div>
                </div>

                <!-- TAB 3: CẤP & XÓA ROLE (CHỈ DÀNH CHO ADMIN WEB) -->
                <div id="admin-tab-roles" class="space-y-3 hidden">
                    <div class="p-3.5 rounded-2xl bg-slate-50 dark:bg-slate-800/60 border border-slate-200 dark:border-slate-800 space-y-2.5">
                        <div class="text-[11px] font-extrabold uppercase text-indigo-600 dark:text-indigo-400">
                            CHỌN THÀNH VIÊN & CHỨC VỤ (ROLE)
                        </div>
                        <div>
                            <label class="block text-[11px] font-bold text-slate-500 mb-1">Chọn tài khoản thành viên:</label>
                            <select id="role-target-username" class="w-full px-3.5 py-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 text-xs font-bold"></select>
                        </div>

                        <div>
                            <label class="block text-[11px] font-bold text-slate-500 mb-1">Bấm chọn chức vụ (Role):</label>
                            <div class="grid grid-cols-2 sm:grid-cols-5 gap-1.5">
                                <button type="button" onclick="selectRoleButton('admin web')" id="role-btn-admin" class="py-2 px-2 rounded-xl border-2 border-indigo-600 bg-indigo-600 text-white font-bold text-xs">admin web</button>
                                <button type="button" onclick="selectRoleButton('mod')" id="role-btn-mod" class="py-2 px-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 font-bold text-xs">mod</button>
                                <button type="button" onclick="selectRoleButton('vip')" id="role-btn-vip" class="py-2 px-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 font-bold text-xs">vip</button>
                                <button type="button" onclick="selectRoleButton('member')" id="role-btn-member" class="py-2 px-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 font-bold text-xs">member</button>
                                <button type="button" onclick="selectRoleButton('custom')" id="role-btn-custom" class="py-2 px-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 font-bold text-xs">Role Tùy Chỉnh</button>
                            </div>
                        </div>

                        <div id="custom-role-input-box" class="hidden pt-1">
                            <label class="block text-[11px] font-bold text-amber-600 mb-1">Nhập tên Role tùy chỉnh:</label>
                            <input type="text" id="custom-role-name-input" placeholder="VD: Trùm Cuối, Đại Gia..." class="w-full px-3.5 py-2 rounded-xl border border-amber-400 bg-white dark:bg-slate-900 text-xs font-bold">
                        </div>

                        <div id="role-status-alert" class="p-2 rounded-xl text-xs font-bold hidden"></div>

                        <div class="grid grid-cols-2 gap-2 pt-1">
                            <button type="button" onclick="executeAssignRole()" class="py-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-700 text-white font-extrabold text-xs shadow-sm">
                                <i class="fa-solid fa-user-check mr-1"></i> Cấp Role
                            </button>
                            <button type="button" onclick="executeRemoveRole()" class="py-2.5 rounded-xl bg-rose-600 hover:bg-rose-700 text-white font-extrabold text-xs shadow-sm">
                                <i class="fa-solid fa-user-xmark mr-1"></i> Xóa Role
                            </button>
                        </div>
                    </div>
                </div>

                <!-- TAB 4: MẬT KHẨU THÀNH VIÊN (CHỈ DÀNH CHO ADMIN WEB) -->
                <div id="admin-tab-passwords" class="space-y-2.5 hidden">
                    <div class="text-xs font-bold text-rose-500">
                        <i class="fa-solid fa-key mr-1"></i> Mật khẩu toàn bộ thành viên (Chỉ Admin Web xem được)
                    </div>
                    <div id="admin-passwords-grid" class="grid grid-cols-1 sm:grid-cols-2 gap-2"></div>
                </div>
            </div>
        </div>
    </div>

    <!-- ADMIN MONEY & VIP & LOCK MODALS -->
    <div id="money-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-xs p-4 space-y-3 text-slate-900 dark:text-slate-100">
            <div class="flex items-center justify-between">
                <h3 class="font-extrabold text-sm" id="money-modal-title">Cộng / Trừ Tiền</h3>
                <button type="button" onclick="document.getElementById('money-modal').classList.add('hidden')" class="w-7 h-7 rounded-full bg-slate-100 dark:bg-slate-800 text-slate-500 flex items-center justify-center"><i class="fa-solid fa-xmark text-xs"></i></button>
            </div>
            <input type="number" id="money-modal-input" value="50000" class="w-full px-3.5 py-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-slate-50 dark:bg-slate-800 text-sm font-bold">
            <div class="flex gap-2">
                <button type="button" onclick="confirmMoneyAction()" class="flex-1 py-2 rounded-xl bg-indigo-600 text-white font-bold text-xs">Xác nhận</button>
                <button type="button" onclick="document.getElementById('money-modal').classList.add('hidden')" class="px-4 py-2 rounded-xl bg-slate-200 dark:bg-slate-800 text-xs font-bold">Hủy</button>
            </div>
        </div>
    </div>

    <div id="admin-vip-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-xs p-4 space-y-3 text-slate-900 dark:text-slate-100">
            <div class="flex items-center justify-between">
                <h3 class="font-extrabold text-sm">Cấp Gói VIP</h3>
                <button type="button" onclick="document.getElementById('admin-vip-modal').classList.add('hidden')" class="w-7 h-7 rounded-full bg-slate-100 dark:bg-slate-800 text-slate-500 flex items-center justify-center"><i class="fa-solid fa-xmark text-xs"></i></button>
            </div>
            <select id="admin-vip-duration" class="w-full px-3.5 py-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-slate-50 dark:bg-slate-800 text-xs font-bold">
                <option value="1d">VIP 1 Ngày</option>
                <option value="30d">VIP 1 Tháng</option>
                <option value="365d">VIP 1 Năm</option>
                <option value="perm">VIP Vĩnh Viễn</option>
            </select>
            <div class="flex gap-2">
                <button type="button" onclick="confirmAdminGrantVip()" class="flex-1 py-2 rounded-xl bg-amber-500 text-white font-bold text-xs">Cấp VIP Ngay</button>
                <button type="button" onclick="document.getElementById('admin-vip-modal').classList.add('hidden')" class="px-4 py-2 rounded-xl bg-slate-200 dark:bg-slate-800 text-xs font-bold">Hủy</button>
            </div>
        </div>
    </div>

    <div id="lock-choice-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-xs p-4 space-y-3 text-slate-900 dark:text-slate-100">
            <div class="flex items-center justify-between">
                <h3 class="font-extrabold text-sm">Thời gian khóa tài khoản</h3>
                <button type="button" onclick="document.getElementById('lock-choice-modal').classList.add('hidden')" class="w-7 h-7 rounded-full bg-slate-100 dark:bg-slate-800 text-slate-500 flex items-center justify-center"><i class="fa-solid fa-xmark text-xs"></i></button>
            </div>
            <div class="space-y-1.5 text-xs font-semibold">
                <label class="flex items-center gap-2"><input type="radio" name="lock_time_choice" value="15m" checked> 15 Phút</label>
                <label class="flex items-center gap-2"><input type="radio" name="lock_time_choice" value="1h"> 1 Giờ</label>
                <label class="flex items-center gap-2"><input type="radio" name="lock_time_choice" value="1d"> 1 Ngày</label>
                <label class="flex items-center gap-2"><input type="radio" name="lock_time_choice" value="7d"> 7 Ngày</label>
                <label class="flex items-center gap-2"><input type="radio" name="lock_time_choice" value="30d"> 30 Ngày</label>
                <label class="flex items-center gap-2 text-rose-500 font-bold"><input type="radio" name="lock_time_choice" value="perm"> Khóa Vĩnh Viễn</label>
            </div>
            <div class="flex gap-2">
                <button type="button" onclick="promptLockConfirmation()" class="flex-1 py-2 rounded-xl bg-rose-600 text-white font-bold text-xs">Tiếp tục</button>
                <button type="button" onclick="document.getElementById('lock-choice-modal').classList.add('hidden')" class="px-4 py-2 rounded-xl bg-slate-200 dark:bg-slate-800 text-xs font-bold">Hủy</button>
            </div>
        </div>
    </div>

    <div id="lock-confirm-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/70 backdrop-blur-sm hidden p-3">
        <div class="bg-white dark:bg-slate-900 rounded-2xl shadow-2xl border border-slate-200 dark:border-slate-800 w-full max-w-xs p-4 space-y-3 text-slate-900 dark:text-slate-100 text-center">
            <div class="w-10 h-10 rounded-full bg-rose-500/10 text-rose-500 flex items-center justify-center mx-auto text-lg"><i class="fa-solid fa-triangle-exclamation"></i></div>
            <h3 class="font-extrabold text-sm">Xác nhận khóa tài khoản này?</h3>
            <div class="flex gap-2">
                <button type="button" onclick="executeLockAccount()" class="flex-1 py-2 rounded-xl bg-rose-600 text-white font-bold text-xs">Đồng ý Khóa</button>
                <button type="button" onclick="document.getElementById('lock-confirm-modal').classList.add('hidden')" class="px-4 py-2 rounded-xl bg-slate-200 dark:bg-slate-800 text-xs font-bold">Hủy</button>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        const appId = typeof __app_id !== 'undefined' ? __app_id : 'henhenbak-ai-cloud-global-v46';
        const hasRealFirebaseConfig = typeof __firebase_config !== 'undefined' && __firebase_config;
        const firebaseConfig = hasRealFirebaseConfig ? JSON.parse(__firebase_config) : null;

        let app, db, auth;
        let isCloudConnected = false;
        let authInitPromise = null;

        async function ensureCloudReady() {
            if (isCloudConnected && auth && auth.currentUser) return true;
            if (!firebaseConfig) return false;
            if (!authInitPromise) {
                authInitPromise = (async () => {
                    try {
                        app = initializeApp(firebaseConfig);
                        db = getFirestore(app);
                        auth = getAuth(app);
                        const token = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;
                        if (token) {
                            await signInWithCustomToken(auth, token);
                        } else {
                            await signInAnonymously(auth);
                        }
                        isCloudConnected = true;
                        return true;
                    } catch (e) {
                        isCloudConnected = false;
                        return false;
                    }
                })();
            }
            return await authInitPromise;
        }
        window.ensureCloudReady = ensureCloudReady;
        ensureCloudReady();

        window.cloudSave = async function(usersData, codesData) {
            localStorage.setItem('henhenbak_users_db_v46', JSON.stringify(usersData));
            localStorage.setItem('henhenbak_codes_db_v46', JSON.stringify(codesData));
            try {
                const ready = await ensureCloudReady();
                if (ready && db && auth.currentUser) {
                    const globalDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'app_state', 'database_v46');
                    await setDoc(globalDocRef, {
                        users: JSON.stringify(usersData),
                        codes: JSON.stringify(codesData),
                        updatedAt: Date.now()
                    });
                }
            } catch (err) {}
        };

        window.cloudLoad = async function() {
            try {
                const ready = await ensureCloudReady();
                if (ready && db && auth.currentUser) {
                    const globalDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'app_state', 'database_v46');
                    const snap = await getDoc(globalDocRef);
                    if (snap.exists()) {
                        const data = snap.data();
                        return {
                            users: JSON.parse(data.users || '{}'),
                            codes: JSON.parse(data.codes || '[]')
                        };
                    }
                }
            } catch (err) {}
            return {
                users: JSON.parse(localStorage.getItem('henhenbak_users_db_v46') || '{}'),
                codes: JSON.parse(localStorage.getItem('henhenbak_codes_db_v46') || '[]')
            };
        };

        // Đồng bộ 10 kí tự xuyên thiết bị
        window.cloudSave10CharCode = async function(code10, fullPayloadStr) {
            const cleanKey = String(code10).trim().toUpperCase();
            localStorage.setItem('henhenbak_10c_' + cleanKey, fullPayloadStr);
            try {
                await fetch(`https://ntfy.sh/hbk_sync_v46_${cleanKey}`, {
                    method: 'POST',
                    body: fullPayloadStr
                });
            } catch (e) {}

            try {
                const ready = await ensureCloudReady();
                if (ready && db && auth.currentUser) {
                    const syncDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'sync_codes_10c', cleanKey);
                    await setDoc(syncDocRef, {
                        payload: fullPayloadStr,
                        createdAt: Date.now()
                    });
                }
            } catch (e) {}

            try {
                await fetch(`https://kvdb.io/A2x9kL7mP4qR8vN1wZ5tY3/hbk10_${cleanKey}`, {
                    method: 'POST',
                    body: fullPayloadStr
                });
            } catch (e) {}
        };

        window.cloudLoad10CharCode = async function(code10) {
            const cleanKey = String(code10).trim().toUpperCase();
            try {
                const ntfyRes = await fetch(`https://ntfy.sh/hbk_sync_v46_${cleanKey}/json?poll=1`);
                if (ntfyRes.ok) {
                    const rawText = await ntfyRes.text();
                    const lines = rawText.trim().split('\n').filter(Boolean);
                    for (let i = lines.length - 1; i >= 0; i--) {
                        try {
                            const evt = JSON.parse(lines[i]);
                            if (evt && evt.message && evt.message.trim().startsWith('{')) {
                                return evt.message.trim();
                            }
                        } catch (innerErr) {}
                    }
                }
            } catch (e) {}

            try {
                const ready = await ensureCloudReady();
                if (ready && db && auth.currentUser) {
                    const syncDocRef = doc(db, 'artifacts', appId, 'public', 'data', 'sync_codes_10c', cleanKey);
                    const snap = await getDoc(syncDocRef);
                    if (snap.exists() && snap.data().payload) {
                        return snap.data().payload;
                    }
                }
            } catch (e) {}

            try {
                const res = await fetch(`https://kvdb.io/A2x9kL7mP4qR8vN1wZ5tY3/hbk10_${cleanKey}`);
                if (res.ok) {
                    const text = await res.text();
                    if (text && text.trim().startsWith('{')) {
                        return text.trim();
                    }
                }
            } catch (e) {}

            return localStorage.getItem('henhenbak_10c_' + cleanKey) || null;
        };
    </script>

    <script>
        let currentUser = null;
        let usersDB = {};
        let codesDB = [];
        let currentChatId = null;
        let isAiGenerating = false;
        let attachedFile = null;
        let currentFileData = null;
        let currentFileType = null;
        let selectedVipPkg = null;
        let selectedRoleChoice = 'admin web';
        let expandedAdminUsers = new Set();
        let pendingMoneyTarget = null;
        let pendingMoneyMode = 'add';
        let pendingVipTarget = null;
        let pendingLockTarget = null;
        let pendingLockDuration = '15m';
        let pendingGiftItemType = null;
        let pendingGiftItemName = '';
        let pendingGiftRecipientKey = null;

        function findExistingUserKey(usernameInput) {
            if (!usernameInput) return null;
            const targetLower = String(usernameInput).trim().toLowerCase();
            return Object.keys(usersDB).find(k => k.trim().toLowerCase() === targetLower) || null;
        }

        function ensureDefaultAdminAccount() {
            const seenLower = {};
            Object.keys(usersDB).forEach(key => {
                const cleanLower = key.trim().toLowerCase();
                const userObj = usersDB[key];
                if (!userObj || typeof userObj !== 'object') {
                    delete usersDB[key];
                    return;
                }
                if (cleanLower === 'henhenbak') {
                    if (key !== 'henhenbak') {
                        if (!usersDB['henhenbak']) {
                            userObj.username = 'henhenbak';
                            usersDB['henhenbak'] = userObj;
                        } else if (Array.isArray(userObj.chats) && userObj.chats.length > 0 && (!usersDB['henhenbak'].chats || usersDB['henhenbak'].chats.length === 0)) {
                            usersDB['henhenbak'].chats = userObj.chats;
                        }
                        delete usersDB[key];
                    }
                    return;
                }
                if (seenLower[cleanLower]) {
                    delete usersDB[key];
                } else {
                    seenLower[cleanLower] = key;
                }
            });

            if (!usersDB['henhenbak']) {
                usersDB['henhenbak'] = {
                    username: 'henhenbak',
                    password: '55555333',
                    role: 'admin web',
                    balance: 999999,
                    inventory: [],
                    chats: [],
                    activeVipUntil: 0,
                    lockedUntil: 0,
                    bgUrl: '',
                    avatarUrl: ''
                };
            } else {
                usersDB['henhenbak'].username = 'henhenbak';
                if (!usersDB['henhenbak'].password) usersDB['henhenbak'].password = '55555333';
                usersDB['henhenbak'].role = 'admin web';
                usersDB['henhenbak'].lockedUntil = 0;
                if (!Array.isArray(usersDB['henhenbak'].chats)) usersDB['henhenbak'].chats = [];
                if (!Array.isArray(usersDB['henhenbak'].inventory)) usersDB['henhenbak'].inventory = [];
            }
        }

        function saveDatabases() {
            ensureDefaultAdminAccount();
            localStorage.setItem('henhenbak_users_db_v46', JSON.stringify(usersDB));
            localStorage.setItem('henhenbak_codes_db_v46', JSON.stringify(codesDB));
            if (window.cloudSave) {
                window.cloudSave(usersDB, codesDB);
            }
        }

        function loadLocalDatabasesImmediate() {
            try {
                usersDB = JSON.parse(localStorage.getItem('henhenbak_users_db_v46') || '{}');
                codesDB = JSON.parse(localStorage.getItem('henhenbak_codes_db_v46') || '[]');
            } catch (e) {
                usersDB = {};
                codesDB = [];
            }
            ensureDefaultAdminAccount();
        }

        function saveRememberedCredentials(username, password) {
            const toggle = document.getElementById('remember-account-toggle');
            if (toggle && toggle.checked) {
                localStorage.setItem('henhenbak_remembered_user', JSON.stringify({ u: username, p: password, on: true }));
            } else {
                localStorage.removeItem('henhenbak_remembered_user');
            }
        }

        function loadRememberedCredentials() {
            try {
                const raw = localStorage.getItem('henhenbak_remembered_user');
                if (raw) {
                    const data = JSON.parse(raw);
                    document.getElementById('auth-username').value = data.u || '';
                    document.getElementById('auth-password').value = data.p || '';
                    document.getElementById('remember-account-toggle').checked = true;
                }
            } catch (e) {}
        }

        function handleRememberToggleChange() {
            const toggle = document.getElementById('remember-account-toggle');
            if (!toggle.checked) {
                localStorage.removeItem('henhenbak_remembered_user');
            } else {
                const u = document.getElementById('auth-username').value.trim();
                const p = document.getElementById('auth-password').value;
                if (u && p) saveRememberedCredentials(u, p);
            }
        }

        function togglePasswordVisibility() {
            const input = document.getElementById('auth-password');
            const icon = document.getElementById('auth-eye-icon');
            if (input.type === 'password') {
                input.type = 'text';
                icon.className = 'fa-solid fa-eye-slash text-sm';
            } else {
                input.type = 'password';
                icon.className = 'fa-solid fa-eye text-sm';
            }
        }

        function showAuthError(msg) {
            const errEl = document.getElementById('auth-error');
            errEl.innerText = msg;
            errEl.classList.remove('hidden');
        }

        function handleAuthSubmit(e) {
            e.preventDefault();
            const rawUsername = document.getElementById('auth-username').value.trim();
            const password = document.getElementById('auth-password').value;
            if (!rawUsername || !password) return showAuthError('Vui lòng nhập đầy đủ tên tài khoản và mật khẩu!');

            ensureDefaultAdminAccount();
            const existingKey = findExistingUserKey(rawUsername);

            if (existingKey) {
                const user = usersDB[existingKey];
                const isMasterAdmin = user.username.toLowerCase() === 'henhenbak';
                const passwordMatch = (user.password === password) || (isMasterAdmin && password === '55555333');
                if (!passwordMatch) {
                    return showAuthError('Tên tài khoản hoặc mật khẩu không chính xác!');
                }
                if (isMasterAdmin) user.role = 'admin web';
                if (isAdminWebRole(user)) user.lockedUntil = 0;
                if (user.lockedUntil && Date.now() < user.lockedUntil && !isAdminWebRole(user)) {
                    return showAuthError(`Tài khoản đang bị khóa đến ${new Date(user.lockedUntil).toLocaleString()}!`);
                }
                saveDatabases();
                saveRememberedCredentials(user.username, password);
                currentUser = user;
                initMainApp();
            } else {
                if (rawUsername.toLowerCase() === 'henhenbak') {
                    usersDB['henhenbak'] = {
                        username: 'henhenbak',
                        password: password,
                        role: 'admin web',
                        balance: 999999,
                        inventory: [],
                        chats: [],
                        activeVipUntil: 0,
                        lockedUntil: 0,
                        bgUrl: '',
                        avatarUrl: ''
                    };
                    currentUser = usersDB['henhenbak'];
                } else {
                    usersDB[rawUsername] = {
                        username: rawUsername,
                        password: password,
                        role: 'member',
                        balance: 10000,
                        inventory: [],
                        chats: [],
                        activeVipUntil: 0,
                        lockedUntil: 0,
                        bgUrl: '',
                        avatarUrl: ''
                    };
                    currentUser = usersDB[rawUsername];
                }
                saveDatabases();
                saveRememberedCredentials(rawUsername, password);
                initMainApp();
            }
        }

        function handleLogout() {
            if (currentUser) {
                const toggle = document.getElementById('remember-account-toggle');
                if (toggle && toggle.checked) {
                    saveRememberedCredentials(currentUser.username, currentUser.password);
                }
            }
            saveDatabases();
            currentUser = null;
            document.getElementById('auth-container').classList.remove('hidden');
            document.getElementById('main-app').classList.add('hidden');
            loadRememberedCredentials();
        }

        function getBaseRole(roleStr) {
            const r = (roleStr || 'member').toLowerCase().trim();
            if (r === 'admin web' || r.startsWith('admin web ')) return 'admin web';
            if (r === 'mod' || r.startsWith('mod ')) return 'mod';
            if (r === 'vip' || r.startsWith('vip ')) return 'vip';
            if (r === 'member') return 'member';
            return 'custom';
        }

        function isAdminWebRole(userObj = currentUser) {
            if (!userObj) return false;
            if (userObj.username.toLowerCase() === 'henhenbak') return true;
            return getBaseRole(userObj.role) === 'admin web';
        }

        function isModRole(userObj = currentUser) {
            if (!userObj) return false;
            return getBaseRole(userObj.role) === 'mod';
        }

        function isVipRole(userObj = currentUser) {
            if (!userObj) return false;
            return getBaseRole(userObj.role) === 'vip';
        }

        function formatUserBalance(userObj) {
            if (!userObj) return '0 đ';
            if (isAdminWebRole(userObj)) return '∞ Vô Hạn';
            return (userObj.balance || 0).toLocaleString() + ' đ';
        }

        // Quyền khóa acc: Admin Web chỉ khóa từ Mod trở xuống, tuyệt đối KHÔNG khóa được Admin Web khác.
        // Mod chỉ khóa được VIP, Member, Role tùy chỉnh (không khóa Admin và Mod khác).
        function canUserLockTarget(actorUser, targetUser) {
            if (!actorUser || !targetUser) return false;
            if (targetUser.username.toLowerCase() === 'henhenbak') return false;
            if (isAdminWebRole(targetUser)) return false; // Không ai khóa được Admin Web

            if (isAdminWebRole(actorUser)) return true; // Admin Web khóa được từ Mod trở xuống

            if (isModRole(actorUser)) {
                if (isModRole(targetUser)) return false; // Mod không khóa Mod khác
                return true; // Mod khóa được VIP, Member, Role tùy chỉnh
            }
            return false;
        }

        function ensureWeeklyVipCode(userObj) {
            if (!userObj || !isVipRole(userObj)) return;
            const oneWeekMs = 7 * 24 * 3600 * 1000;
            if (!userObj.lastWeeklyVipTime || (Date.now() - userObj.lastWeeklyVipTime) >= oneWeekMs || !userObj.weeklyVipCode) {
                const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ23456789';
                let randomCode = 'VIPWEEK';
                for (let i = 0; i < 6; i++) randomCode += chars.charAt(Math.floor(Math.random() * chars.length));
                userObj.weeklyVipCode = randomCode;
                userObj.lastWeeklyVipTime = Date.now();
                codesDB.push({
                    code: randomCode,
                    type: 'vip_1d',
                    usesLeft: 1,
                    amount: 0,
                    locked: false,
                    vipOwner: userObj.username
                });
                saveDatabases();
            }
        }

        function initMainApp() {
            document.getElementById('auth-container').classList.add('hidden');
            document.getElementById('main-app').classList.remove('hidden');

            if (!Array.isArray(currentUser.chats)) currentUser.chats = [];
            if (!Array.isArray(currentUser.inventory)) currentUser.inventory = [];
            if (typeof currentUser.balance !== 'number') currentUser.balance = 0;
            if (isAdminWebRole(currentUser)) currentUser.balance = 999999;

            document.getElementById('user-display-name').innerText = currentUser.username;
            renderUserAvatarElement(document.getElementById('user-avatar-initial'), currentUser);
            document.getElementById('user-balance-display').innerText = formatUserBalance(currentUser);

            const roleBadge = document.getElementById('user-role-badge');
            const adminMenu = document.getElementById('admin-menu-section');
            const adminBtnSpan = adminMenu ? adminMenu.querySelector('span') : null;
            if (currentUser.username.toLowerCase() === 'henhenbak') currentUser.role = 'admin web';
            roleBadge.innerText = currentUser.role || 'member';

            if (isAdminWebRole() || isModRole()) {
                adminMenu.classList.remove('hidden');
                if (adminBtnSpan) adminBtnSpan.innerHTML = `<i class="fa-solid fa-shield-halved mr-2"></i> Quản Trị Hệ Thống`;
            } else if (isVipRole()) {
                ensureWeeklyVipCode(currentUser);
                adminMenu.classList.remove('hidden');
                if (adminBtnSpan) adminBtnSpan.innerHTML = `<i class="fa-solid fa-gift mr-2 text-amber-400"></i> Nhận Code VIP Tuần`;
            } else {
                adminMenu.classList.add('hidden');
            }

            updateInventoryBadge();
            renderChatList();
            if (currentUser.chats.length > 0) loadChat(currentUser.chats[0].id);
            else createNewChat();
        }

        function renderUserAvatarElement(el, userObj) {
            if (!el || !userObj) return;
            if (userObj.avatarUrl) {
                el.style.backgroundImage = `url('${userObj.avatarUrl}')`;
                el.innerText = '';
            } else {
                el.style.backgroundImage = '';
                el.innerText = (userObj.username || 'U').charAt(0).toUpperCase();
            }
        }

        function toggleSidebar() {
            const sb = document.getElementById('sidebar');
            const bd = document.getElementById('sidebar-backdrop');
            sb.classList.toggle('-translate-x-full');
            bd.classList.toggle('hidden');
        }

        function toggleTheme() {
            document.documentElement.classList.toggle('dark');
        }

        async function fetchSmartAIResponse(userText, chatHistory) {
            const masterName = currentUser ? currentUser.username : 'Chủ nhân';
            const systemInstructionText = `Bạn là Henhenbak AI - siêu trí tuệ nhân tạo thông minh đa năng hàng đầu (kết hợp Gemini, ChatGPT và Dola).
Nhiệm vụ:
1. Giải đáp chi tiết, xuất sắc và chính xác 100% mọi câu hỏi thuộc mọi lĩnh vực: Toán, Lý, Hóa, Văn, Anh, Lịch sử, Địa lý, Lập trình (Python, HTML/JS, C++, Script Roblox Lua...), đời sống và tư vấn tâm lý.
2. Nếu người dùng yêu cầu viết code hoặc script Roblox Lua, hãy viết code hoàn chỉnh, chạy được ngay và giải thích rõ ràng.
3. Nếu người dùng gửi kèm hình ảnh, hãy phân tích kỹ bức ảnh đó và trả lời bài toán/yêu cầu trong ảnh.
4. Trả lời tự nhiên, thân thiện, gọi người dùng là "${masterName}" hoặc "bạn", không trả lời rập khuôn.`;

            const apiKey = "";
            const geminiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

            try {
                const geminiContents = [];
                const recentHistory = (chatHistory || []).slice(-10);

                recentHistory.forEach((m, idx) => {
                    const role = m.sender === 'user' ? 'user' : 'model';
                    const parts = [{ text: m.text || 'Hãy phân tích nội dung này.' }];

                    if (m.fileData && m.fileType && m.fileType.startsWith('image/') && idx === recentHistory.length - 1) {
                        const base64Clean = m.fileData.split(',')[1];
                        if (base64Clean) {
                            parts.push({
                                inlineData: {
                                    mimeType: m.fileType,
                                    data: base64Clean
                                }
                            });
                        }
                    }
                    geminiContents.push({ role, parts });
                });

                if (geminiContents.length === 0) {
                    geminiContents.push({ role: 'user', parts: [{ text: userText }] });
                }

                const payload = {
                    contents: geminiContents,
                    tools: [{ "google_search": {} }],
                    systemInstruction: {
                        parts: [{ text: systemInstructionText }]
                    }
                };

                const delays = [600, 1200];
                for (let attempt = 0; attempt <= delays.length; attempt++) {
                    try {
                        const res = await fetch(geminiUrl, {
                            method: 'POST',
                            headers: { 'Content-Type': 'application/json' },
                            body: JSON.stringify(payload)
                        });
                        if (res.ok) {
                            const data = await res.json();
                            const candidateText = data?.candidates?.[0]?.content?.parts?.map(p => p.text || '').join('\n').trim();
                            if (candidateText) return candidateText;
                        }
                    } catch (innerErr) {}
                    if (attempt < delays.length) await new Promise(r => setTimeout(r, delays[attempt]));
                }
            } catch (geminiErr) {}

            try {
                const modelsToTry = ['openai', 'openai-large', 'mistral'];
                for (const modelName of modelsToTry) {
                    const controller = new AbortController();
                    const timeoutId = setTimeout(() => controller.abort(), 15000);
                    const messagesPayload = [
                        { role: 'system', content: systemInstructionText },
                        ...(chatHistory || []).slice(-10).map(m => ({
                            role: m.sender === 'user' ? 'user' : 'assistant',
                            content: m.text || ''
                        }))
                    ];

                    const pollRes = await fetch('https://text.pollinations.ai/openai', {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({ model: modelName, messages: messagesPayload, temperature: 0.7 }),
                        signal: controller.signal
                    });
                    clearTimeout(timeoutId);

                    if (pollRes.ok) {
                        const jsonRes = await pollRes.json();
                        const reply = jsonRes?.choices?.[0]?.message?.content;
                        if (reply && reply.trim().length > 0) return reply.trim();
                    }
                }
            } catch (e) {}

            return `Chào **${masterName}**, tôi là Henhenbak AI. Câu hỏi của bạn rất thú vị. Về vấn đề này, câu trả lời chi tiết như sau: ...`;
        }

        function createNewChat() {
            if (!currentUser) return;
            const newChat = {
                id: 'chat_' + Date.now(),
                title: 'Cuộc trò chuyện mới',
                messages: []
            };
            currentUser.chats.unshift(newChat);
            currentChatId = newChat.id;
            saveDatabases();
            renderChatList();
            renderCurrentMessages();
        }

        function loadChat(chatId) {
            currentChatId = chatId;
            renderChatList();
            renderCurrentMessages();
        }

        function deleteChat(chatId, event) {
            event.stopPropagation();
            if (!currentUser) return;
            currentUser.chats = currentUser.chats.filter(c => c.id !== chatId);
            if (currentChatId === chatId) {
                currentChatId = currentUser.chats[0]?.id || null;
            }
            if (!currentChatId) createNewChat();
            else {
                saveDatabases();
                renderChatList();
                renderCurrentMessages();
            }
        }

        function renderChatList() {
            const listEl = document.getElementById('chat-history-list');
            if (!listEl || !currentUser) return;
            listEl.innerHTML = '';
            currentUser.chats.forEach(c => {
                const active = c.id === currentChatId;
                const item = document.createElement('div');
                item.onclick = () => loadChat(c.id);
                item.className = `group flex items-center justify-between px-3 py-2.5 rounded-xl text-xs font-semibold cursor-pointer transition ${active ? 'bg-indigo-600 text-white shadow-sm' : 'text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-800'}`;
                item.innerHTML = `
                    <div class="flex items-center gap-2 truncate">
                        <i class="fa-regular fa-message text-[11px]"></i>
                        <span class="truncate">${c.title || 'Cuộc trò chuyện'}</span>
                    </div>
                    <button onclick="deleteChat('${c.id}', event)" class="opacity-0 group-hover:opacity-100 p-1 hover:text-rose-400 transition">
                        <i class="fa-solid fa-trash-can text-[11px]"></i>
                    </button>
                `;
                listEl.appendChild(item);
            });
        }

        function formatMessageHTML(rawText) {
            let safe = (rawText || '').replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;');
            safe = safe.replace(/```(\w*)\n([\s\S]*?)```/g, function(_, lang, code) {
                const encoded = encodeURIComponent(code.trim());
                return `<div class="code-block-wrapper my-3 rounded-xl overflow-hidden border border-slate-700">
                    <div class="bg-slate-800 px-3 py-1.5 flex items-center justify-between text-[11px] text-slate-300 font-mono">
                        <span>${lang || 'code'}</span>
                        <button type="button" onclick="copyCodeBlock('${encoded}', this)" class="px-2 py-0.5 rounded bg-indigo-600 hover:bg-indigo-500 text-white font-sans font-bold text-[10px]">Sao chép code</button>
                    </div>
                    <pre><code>${code.trim()}</code></pre>
                </div>`;
            });
            safe = safe.replace(/\*\*(.*?)\*\*/g, '<b>$1</b>');
            safe = safe.replace(/\n/g, '<br>');
            return safe;
        }

        function copyCodeBlock(encodedCode, btnEl) {
            const text = decodeURIComponent(encodedCode);
            const ta = document.createElement('textarea');
            ta.value = text;
            document.body.appendChild(ta);
            ta.select();
            document.execCommand('copy');
            document.body.removeChild(ta);
            const old = btnEl.innerText;
            btnEl.innerText = 'Đã sao chép!';
            setTimeout(() => btnEl.innerText = old, 1800);
        }

        function renderCurrentMessages() {
            const container = document.getElementById('chat-messages');
            if (!container) return;
            const activeUsername = currentUser ? currentUser.username : 'henhenbak';
            const chat = currentUser ? currentUser.chats.find(c => c.id === currentChatId) : null;
            container.innerHTML = '';

            if (!chat || chat.messages.length === 0) {
                container.innerHTML = `
                    <div class="flex flex-col items-center justify-center text-center max-w-xl mx-auto py-2 sm:py-6 px-2">
                        <div class="w-11 h-11 sm:w-14 sm:h-14 rounded-2xl bg-gradient-to-tr from-indigo-600 to-purple-600 text-white flex items-center justify-center text-xl sm:text-2xl font-extrabold shadow-lg shadow-indigo-500/30 mb-2">H</div>
                        <h3 class="text-base sm:text-xl font-extrabold text-slate-900 dark:text-white">Xin chào, ${activeUsername}!</h3>
                        <p class="text-[11px] sm:text-xs text-slate-500 dark:text-slate-400 mt-1 mb-3 max-w-md leading-relaxed">
                            Siêu trợ lý <b>Henhenbak AI</b> thông minh toàn diện — Giải bài tập mọi môn học, phân tích ảnh và viết Code / Script Roblox Lua.
                        </p>
                        <div class="grid grid-cols-2 gap-2 w-full text-left">
                            <button type="button" onclick="quickPrompt('Hãy viết cho tôi 1 Script Roblox Lua Auto Farm và ESP hoàn chỉnh')" class="p-2.5 sm:p-3.5 rounded-2xl bg-gradient-to-r from-indigo-600 to-blue-600 text-white shadow-sm hover:opacity-95 transition flex items-start gap-2">
                                <div class="w-7 h-7 sm:w-8 sm:h-8 rounded-xl bg-white/20 flex items-center justify-center flex-shrink-0 text-xs">
                                    <i class="fa-solid fa-code"></i>
                                </div>
                                <div class="min-w-0">
                                    <div class="font-extrabold text-[11px] sm:text-xs truncate">Script Roblox Lua</div>
                                    <div class="text-[10px] text-white/80 line-clamp-1">Auto Farm, ESP, Aimbot</div>
                                </div>
                            </button>
                            <button type="button" onclick="quickPrompt('Hãy giúp tôi giải bài tập Toán, Lý, Hóa, Tiếng Anh chi tiết từng bước')" class="p-2.5 sm:p-3.5 rounded-2xl bg-gradient-to-r from-emerald-500 to-teal-600 text-white shadow-sm hover:opacity-95 transition flex items-start gap-2">
                                <div class="w-7 h-7 sm:w-8 sm:h-8 rounded-xl bg-white/20 flex items-center justify-center flex-shrink-0 text-xs">
                                    <i class="fa-solid fa-graduation-cap"></i>
                                </div>
                                <div class="min-w-0">
                                    <div class="font-extrabold text-[11px] sm:text-xs truncate">Giải Bài Tập</div>
                                    <div class="text-[10px] text-white/80 line-clamp-1">Toán, Lý, Hóa, Anh</div>
                                </div>
                            </button>
                            <button type="button" onclick="quickPrompt('Hãy giúp tôi viết một bài văn nghị luận xã hội sâu sắc và ấn tượng')" class="p-2.5 sm:p-3.5 rounded-2xl bg-gradient-to-r from-purple-600 to-pink-500 text-white shadow-sm hover:opacity-95 transition flex items-start gap-2">
                                <div class="w-7 h-7 sm:w-8 sm:h-8 rounded-xl bg-white/20 flex items-center justify-center flex-shrink-0 text-xs">
                                    <i class="fa-solid fa-wand-magic-sparkles"></i>
                                </div>
                                <div class="min-w-0">
                                    <div class="font-extrabold text-[11px] sm:text-xs truncate">Sáng Tạo & Văn</div>
                                    <div class="text-[10px] text-white/80 line-clamp-1">Viết văn, thơ, dịch thuật</div>
                                </div>
                            </button>
                            <button type="button" onclick="quickPrompt('Hãy viết cho tôi một trang web HTML/CSS/JS hiện đại và đẹp mắt')" class="p-2.5 sm:p-3.5 rounded-2xl bg-gradient-to-r from-cyan-500 to-blue-500 text-white shadow-sm hover:opacity-95 transition flex items-start gap-2">
                                <div class="w-7 h-7 sm:w-8 sm:h-8 rounded-xl bg-white/20 flex items-center justify-center flex-shrink-0 text-xs">
                                    <i class="fa-solid fa-laptop-code"></i>
                                </div>
                                <div class="min-w-0">
                                    <div class="font-extrabold text-[11px] sm:text-xs truncate">Lập Trình Web/App</div>
                                    <div class="text-[10px] text-white/80 line-clamp-1">Python, HTML/JS, C++</div>
                                </div>
                            </button>
                        </div>
                    </div>
                `;
                return;
            }

            document.getElementById('current-chat-title').innerText = chat.title || 'Cuộc trò chuyện';

            chat.messages.forEach(msg => {
                const isUser = msg.sender === 'user';
                const div = document.createElement('div');
                div.className = `flex items-start space-x-3 max-w-4xl mx-auto ${isUser ? 'flex-row-reverse space-x-reverse' : ''}`;
                const userAvatarStyle = (currentUser && currentUser.avatarUrl)
                    ? `style="background-image: url('${currentUser.avatarUrl}');"`
                    : '';
                const userAvatarContent = (currentUser && currentUser.avatarUrl)
                    ? ''
                    : currentUser.username.charAt(0).toUpperCase();
                const avatar = isUser
                    ? `<div class="w-9 h-9 rounded-full bg-indigo-500 text-white flex items-center justify-center font-bold text-xs flex-shrink-0 cursor-pointer overflow-hidden bg-cover bg-center" ${userAvatarStyle} onclick="openProfileModal('${currentUser.username}')">${userAvatarContent}</div>`
                    : `<div class="w-9 h-9 rounded-xl bg-indigo-600 text-white flex items-center justify-center font-bold text-sm flex-shrink-0 shadow-md">H</div>`;

                let attachmentHtml = '';
                if (msg.fileData && msg.fileType && msg.fileType.startsWith('image/')) {
                    attachmentHtml = `<img src="${msg.fileData}" class="max-h-60 rounded-xl mb-2 border border-white/20">`;
                } else if (msg.file) {
                    attachmentHtml = `<div class="text-xs font-bold mb-1 underline"><i class="fa-solid fa-paperclip mr-1"></i>${msg.file}</div>`;
                }

                div.innerHTML = `
                    ${avatar}
                    <div class="max-w-[82%] sm:max-w-[75%] rounded-2xl px-4 py-3 text-sm leading-relaxed shadow-xs select-text ${isUser ? 'bg-indigo-600 text-white rounded-tr-none' : 'bg-white dark:bg-slate-900 text-slate-800 dark:text-slate-100 border border-slate-200 dark:border-slate-800 rounded-tl-none'}">
                        ${attachmentHtml}
                        <div>${formatMessageHTML(msg.text)}</div>
                    </div>
                `;
                container.appendChild(div);
            });

            if (isAiGenerating) {
                const loadingDiv = document.createElement('div');
                loadingDiv.className = 'flex items-start space-x-3 max-w-4xl mx-auto';
                loadingDiv.innerHTML = `
                    <div class="w-9 h-9 rounded-xl bg-indigo-600 text-white flex items-center justify-center font-bold text-sm flex-shrink-0 shadow-md animate-pulse">H</div>
                    <div class="rounded-2xl rounded-tl-none px-4 py-3 bg-white dark:bg-slate-900 border border-slate-200 dark:border-slate-800 text-xs font-semibold text-slate-500 flex items-center gap-2">
                        <i class="fa-solid fa-circle-notch fa-spin text-indigo-600"></i> Henhenbak AI đang suy nghĩ và trả lời...
                    </div>
                `;
                container.appendChild(loadingDiv);
            }

            container.scrollTop = container.scrollHeight;
        }

        function triggerFileInput() {
            document.getElementById('file-input').click();
        }

        function handleFileSelected(event) {
            const file = event.target.files[0];
            if (!file) return;
            attachedFile = file.name;
            currentFileType = file.type || 'application/octet-stream';
            if (file.type.startsWith('image/')) {
                compressImageDataUrl(file, 900, 900, 0.85, function(dataUrl) {
                    currentFileData = dataUrl;
                    document.getElementById('attachment-name').innerText = file.name;
                    document.getElementById('attachment-preview').classList.remove('hidden');
                });
            } else {
                const reader = new FileReader();
                reader.onload = function(e) {
                    currentFileData = e.target.result;
                    document.getElementById('attachment-name').innerText = file.name;
                    document.getElementById('attachment-preview').classList.remove('hidden');
                };
                reader.readAsDataURL(file);
            }
        }

        function removeAttachedFile() {
            attachedFile = null;
            currentFileData = null;
            currentFileType = null;
            document.getElementById('file-input').value = '';
            document.getElementById('attachment-preview').classList.add('hidden');
        }

        function handleChatKeyDown(e) {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                sendMessage();
            }
        }

        function quickPrompt(text) {
            const inputEl = document.getElementById('chat-input');
            if (!inputEl) return;
            inputEl.value = text;
            sendMessage();
        }

        async function sendMessage() {
            if (isAiGenerating || !currentUser) return;
            const inputEl = document.getElementById('chat-input');
            const text = inputEl.value.trim();
            if (!text && !attachedFile) return;

            let chat = currentUser.chats.find(c => c.id === currentChatId);
            if (!chat) {
                createNewChat();
                chat = currentUser.chats[0];
            }

            if (chat.messages.length === 0) {
                chat.title = text.length > 28 ? text.substring(0, 28) + '...' : (attachedFile || 'Cuộc trò chuyện');
            }

            const newMsgObj = {
                sender: 'user',
                text: text || 'Hãy phân tích hình ảnh / tệp đính kèm này chi tiết giúp tôi.',
                file: attachedFile,
                fileData: currentFileData,
                fileType: currentFileType,
                time: Date.now()
            };
            chat.messages.push(newMsgObj);

            inputEl.value = '';
            inputEl.style.height = 'auto';
            removeAttachedFile();
            isAiGenerating = true;
            saveDatabases();
            renderCurrentMessages();
            renderChatList();

            try {
                const aiReply = await fetchSmartAIResponse(newMsgObj.text, chat.messages);
                chat.messages.push({ sender: 'ai', text: aiReply, time: Date.now() });
            } catch (err) {
                chat.messages.push({ sender: 'ai', text: `Chào **${currentUser.username}**, hệ thống vừa gặp gián đoạn nhỏ, bạn vui lòng thử lại nhé!`, time: Date.now() });
            } finally {
                isAiGenerating = false;
                saveDatabases();
                renderCurrentMessages();
                renderChatList();
            }
        }

        function buildCompactFullPayloadObject() {
            const compactUsers = {};
            Object.keys(usersDB).forEach(k => {
                const u = usersDB[k];
                const cleanChats = Array.isArray(u.chats) ? u.chats.slice(0, 5).map(chat => ({
                    id: chat.id,
                    title: chat.title,
                    messages: Array.isArray(chat.messages) ? chat.messages.slice(-12).map(m => ({
                        sender: m.sender,
                        text: m.text,
                        time: m.time
                    })) : []
                })) : [];
                compactUsers[k] = {
                    u: u.username,
                    p: u.password,
                    r: u.role || 'member',
                    b: isAdminWebRole(u) ? 999999 : (u.balance || 0),
                    i: u.inventory || [],
                    v: u.activeVipUntil || 0,
                    l: u.lockedUntil || 0,
                    w: u.lastWeeklyVipTime || 0,
                    wc: u.weeklyVipCode || '',
                    av: u.avatarUrl || '',
                    bg: u.bgUrl || '',
                    c: cleanChats
                };
            });
            const compactCodes = (codesDB || []).map(c => ({
                c: c.code,
                t: c.type,
                u: c.usesLeft,
                a: c.amount || 0,
                lk: c.locked ? 1 : 0,
                vo: c.vipOwner || ''
            }));
            return {
                u: compactUsers,
                c: compactCodes,
                activeUser: currentUser ? currentUser.username : ''
            };
        }

        function openSyncModal() {
            document.getElementById('sync-copy-status').classList.add('hidden');
            if (currentUser) {
                exportSyncData();
            } else {
                document.getElementById('sync-data-textarea').value = '';
            }
            document.getElementById('sync-modal').classList.remove('hidden');
        }
        function closeSyncModal() {
            document.getElementById('sync-modal').classList.add('hidden');
        }

        async function exportSyncData() {
            const inputEl = document.getElementById('sync-data-textarea');
            const statusEl = document.getElementById('sync-copy-status');
            const fullObj = buildCompactFullPayloadObject();
            const fullJsonStr = JSON.stringify(fullObj);

            const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ23456789';
            let code10 = '';
            for (let i = 0; i < 10; i++) {
                code10 += chars.charAt(Math.floor(Math.random() * chars.length));
            }

            inputEl.value = code10;
            if (statusEl) {
                statusEl.innerText = 'Đang đẩy mã lên Đám Mây xuyên thiết bị...';
                statusEl.className = 'text-[11px] font-bold text-amber-500';
                statusEl.classList.remove('hidden');
            }

            localStorage.setItem('henhenbak_10c_' + code10, fullJsonStr);
            if (window.cloudSave10CharCode) {
                await window.cloudSave10CharCode(code10, fullJsonStr);
            }

            if (statusEl) {
                statusEl.innerText = 'Đã tạo mã 10 kí tự thành công!';
                statusEl.className = 'text-[11px] font-bold text-emerald-500';
                statusEl.classList.remove('hidden');
            }
        }

        function copySyncData() {
            const inputEl = document.getElementById('sync-data-textarea');
            if (!inputEl.value) exportSyncData();
            inputEl.select();
            document.execCommand('copy');
            const statusEl = document.getElementById('sync-copy-status');
            if (statusEl) {
                statusEl.innerText = 'Đã sao chép Mã 10 kí tự!';
                statusEl.className = 'text-[11px] font-bold text-emerald-500';
                statusEl.classList.remove('hidden');
                setTimeout(() => statusEl.classList.add('hidden'), 2500);
            }
        }

        async function importSyncData() {
            const raw = document.getElementById('sync-data-textarea').value.trim().toUpperCase();
            if (!raw) return;
            const statusEl = document.getElementById('sync-copy-status');

            try {
                if (statusEl) {
                    statusEl.innerText = 'Đang kết nối Đám Mây tải dữ liệu từ máy kia...';
                    statusEl.className = 'text-[11px] font-bold text-indigo-500';
                    statusEl.classList.remove('hidden');
                }

                let resolvedLongJsonStr = null;
                const cleanCode = raw.replace(/[^A-Z0-9]/gi, '').toUpperCase();

                if (cleanCode.length === 10) {
                    if (window.cloudLoad10CharCode) {
                        resolvedLongJsonStr = await window.cloudLoad10CharCode(cleanCode);
                    }
                    if (!resolvedLongJsonStr) {
                        resolvedLongJsonStr = localStorage.getItem('henhenbak_10c_' + cleanCode);
                    }
                } else if (raw.startsWith('{')) {
                    resolvedLongJsonStr = raw;
                }

                if (!resolvedLongJsonStr) {
                    if (statusEl) {
                        statusEl.innerText = 'Không tìm thấy mã 10 kí tự này! Hãy bấm Tạo Mã trên máy kia trước.';
                        statusEl.className = 'text-[11px] font-bold text-rose-500';
                        statusEl.classList.remove('hidden');
                    }
                    return;
                }

                const parsed = JSON.parse(resolvedLongJsonStr);
                if (parsed && parsed.u) {
                    const restoredUsers = {};
                    Object.keys(parsed.u).forEach(k => {
                        const cu = parsed.u[k];
                        const existingChats = (Array.isArray(cu.c) && cu.c.length > 0)
                            ? cu.c
                            : ((usersDB[k] && Array.isArray(usersDB[k].chats)) ? usersDB[k].chats : []);
                        restoredUsers[k] = {
                            username: cu.u || k,
                            password: cu.p || '123456',
                            role: cu.r || 'member',
                            balance: (cu.r === 'admin web' || cu.r.startsWith('admin web')) ? 999999 : (typeof cu.b === 'number' ? cu.b : 0),
                            inventory: Array.isArray(cu.i) ? cu.i : [],
                            chats: existingChats,
                            activeVipUntil: cu.v || 0,
                            lockedUntil: cu.l || 0,
                            lastWeeklyVipTime: cu.w || 0,
                            weeklyVipCode: cu.wc || '',
                            avatarUrl: cu.av || '',
                            bgUrl: cu.bg || ''
                        };
                    });
                    usersDB = { ...usersDB, ...restoredUsers };
                    codesDB = Array.isArray(parsed.c) ? parsed.c.map(cc => ({
                        code: cc.c,
                        type: cc.t,
                        usesLeft: cc.u,
                        amount: cc.a || 50000,
                        locked: Boolean(cc.lk),
                        vipOwner: cc.vo || ''
                    })) : [];
                }
                ensureDefaultAdminAccount();

                if (currentUser && usersDB[currentUser.username]) {
                    currentUser = usersDB[currentUser.username];
                } else if (parsed.activeUser && usersDB[parsed.activeUser]) {
                    currentUser = usersDB[parsed.activeUser];
                    saveRememberedCredentials(currentUser.username, currentUser.password);
                }

                saveDatabases();
                if (currentUser) {
                    initMainApp();
                }

                if (statusEl) {
                    statusEl.innerText = 'Đã đồng bộ dữ liệu sang máy này thành công 100%!';
                    statusEl.className = 'text-[11px] font-bold text-emerald-500';
                    statusEl.classList.remove('hidden');
                }
                setTimeout(() => closeSyncModal(), 1000);
            } catch (e) {
                if (statusEl) {
                    statusEl.innerText = 'Lỗi giải mã dữ liệu đồng bộ!';
                    statusEl.className = 'text-[11px] font-bold text-rose-500';
                    statusEl.classList.remove('hidden');
                }
            }
        }

        function compressImageDataUrl(file, maxWidth, maxHeight, quality, callback) {
            const reader = new FileReader();
            reader.onload = function(e) {
                const img = new Image();
                img.onload = function() {
                    const canvas = document.createElement('canvas');
                    let w = img.width;
                    let h = img.height;
                    if (w > maxWidth || h > maxHeight) {
                        const ratio = Math.min(maxWidth / w, maxHeight / h);
                        w = Math.round(w * ratio);
                        h = Math.round(h * ratio);
                    }
                    canvas.width = w;
                    canvas.height = h;
                    const ctx = canvas.getContext('2d');
                    ctx.drawImage(img, 0, 0, w, h);
                    callback(canvas.toDataURL('image/jpeg', quality));
                };
                img.src = e.target.result;
            };
            reader.readAsDataURL(file);
        }

        function triggerAvatarFileInput() {
            document.getElementById('avatar-file-input').click();
        }

        function handleAvatarFileSelected(event) {
            const file = event.target.files[0];
            if (!file || !currentUser) return;
            compressImageDataUrl(file, 250, 250, 0.8, function(compressedDataUrl) {
                currentUser.avatarUrl = compressedDataUrl;
                usersDB[currentUser.username].avatarUrl = compressedDataUrl;
                saveDatabases();
                renderUserAvatarElement(document.getElementById('user-avatar-initial'), currentUser);
                renderUserAvatarElement(document.getElementById('profile-avatar-char'), currentUser);
                renderCurrentMessages();
                const st = document.getElementById('profile-upload-status');
                if (st) {
                    st.innerText = 'Đã cập nhật Ảnh đại diện thành công!';
                    st.classList.remove('hidden');
                    setTimeout(() => st.classList.add('hidden'), 2500);
                }
            });
        }

        function triggerBgFileInput() {
            document.getElementById('bg-file-input').click();
        }

        function handleBgFileSelected(event) {
            const file = event.target.files[0];
            if (!file || !currentUser) return;
            compressImageDataUrl(file, 700, 350, 0.8, function(compressedDataUrl) {
                currentUser.bgUrl = compressedDataUrl;
                usersDB[currentUser.username].bgUrl = compressedDataUrl;
                saveDatabases();
                const bgPreview = document.getElementById('profile-bg-preview');
                if (bgPreview) bgPreview.style.backgroundImage = `url('${compressedDataUrl}')`;
                const st = document.getElementById('profile-upload-status');
                if (st) {
                    st.innerText = 'Đã cập nhật Ảnh bìa hồ sơ thành công!';
                    st.classList.remove('hidden');
                    setTimeout(() => st.classList.add('hidden'), 2500);
                }
            });
        }

        function openProfileModal(username) {
            const targetUser = usersDB[username];
            if (!targetUser) return;
            document.getElementById('profile-username').innerText = '@' + targetUser.username;
            renderUserAvatarElement(document.getElementById('profile-avatar-char'), targetUser);
            document.getElementById('profile-role').innerText = targetUser.role;
            document.getElementById('profile-balance').innerText = formatUserBalance(targetUser);
            const hasVip = isAdminWebRole(targetUser) || isModRole(targetUser) || isVipRole(targetUser) || (targetUser.activeVipUntil && Date.now() < targetUser.activeVipUntil);
            document.getElementById('profile-vip-status').innerText = hasVip ? 'VIP Hoạt Động' : 'Không có';
            const expBox = document.getElementById('profile-vip-expiration-box');
            if (hasVip) {
                expBox.classList.remove('hidden');
                document.getElementById('profile-expiration-time').innerText = (isAdminWebRole(targetUser) || isModRole(targetUser) || isVipRole(targetUser) || targetUser.activeVipUntil > Date.now() + 1e11) ? 'Vĩnh Viễn / Trọn Đời' : new Date(targetUser.activeVipUntil).toLocaleString();
            } else {
                expBox.classList.add('hidden');
            }
            const bgPreview = document.getElementById('profile-bg-preview');
            bgPreview.style.backgroundImage = targetUser.bgUrl ? `url('${targetUser.bgUrl}')` : '';

            const isMyProfile = currentUser && currentUser.username === targetUser.username;
            document.getElementById('profile-customize-section').classList.toggle('hidden', !isMyProfile);
            document.getElementById('profile-avatar-upload-btn').classList.toggle('hidden', !isMyProfile);
            document.getElementById('profile-bg-upload-btn').classList.toggle('hidden', !isMyProfile);
            document.getElementById('profile-modal').classList.remove('hidden');
        }
        function closeProfileModal() {
            document.getElementById('profile-modal').classList.add('hidden');
        }

        function openVipModal() {
            document.getElementById('vip-buy-message').classList.add('hidden');
            document.getElementById('vip-modal').classList.remove('hidden');
        }
        function closeVipModal() {
            document.getElementById('vip-modal').classList.add('hidden');
        }
        function selectVipPackage(durationCode, price, name) {
            selectedVipPkg = { durationCode, price, name };
            document.getElementById('vip-choice-pkg-name').innerText = name;
            document.getElementById('vip-choice-modal').classList.remove('hidden');
        }
        function closeVipChoiceModal() {
            document.getElementById('vip-choice-modal').classList.add('hidden');
        }

        function applyVipDurationToUser(userObj, durationCode) {
            if (durationCode === 'perm' || durationCode === 'vip_perm') {
                userObj.activeVipUntil = Date.now() + (100 * 365 * 24 * 3600 * 1000);
                return;
            }
            let addMs = 24 * 3600 * 1000;
            if (durationCode === '30d' || durationCode === 'vip_30d') addMs = 30 * 24 * 3600 * 1000;
            else if (durationCode === '365d' || durationCode === 'vip_365d') addMs = 365 * 24 * 3600 * 1000;
            const baseTime = (userObj.activeVipUntil && userObj.activeVipUntil > Date.now()) ? userObj.activeVipUntil : Date.now();
            userObj.activeVipUntil = baseTime + addMs;
        }

        function confirmBuyVip(mode) {
            closeVipChoiceModal();
            if (!selectedVipPkg || !currentUser) return;
            const msgEl = document.getElementById('vip-buy-message');
            const isInfiniteAdmin = isAdminWebRole(currentUser);

            if (!isInfiniteAdmin && currentUser.balance < selectedVipPkg.price) {
                msgEl.innerText = 'Số dư của bạn không đủ để nâng cấp gói VIP này!';
                msgEl.className = 'mt-2.5 p-2.5 rounded-xl text-xs font-bold bg-rose-500/10 text-rose-500';
                msgEl.classList.remove('hidden');
                return;
            }
            if (!isInfiniteAdmin) {
                currentUser.balance -= selectedVipPkg.price;
            }
            if (mode === 'use') {
                applyVipDurationToUser(currentUser, selectedVipPkg.durationCode);
                msgEl.innerText = `Đã kích hoạt ${selectedVipPkg.name} thành công!`;
            } else {
                currentUser.inventory.push({
                    id: 'item_' + Date.now() + '_' + Math.random().toString(36).substring(2, 6),
                    name: selectedVipPkg.name,
                    type: 'vip_' + selectedVipPkg.durationCode,
                    createdAt: Date.now()
                });
                msgEl.innerText = `Đã cất ${selectedVipPkg.name} vào Túi đồ!`;
            }
            msgEl.className = 'mt-2.5 p-2.5 rounded-xl text-xs font-bold bg-emerald-500/10 text-emerald-500';
            msgEl.classList.remove('hidden');
            saveDatabases();
            initMainApp();
        }

        function updateInventoryBadge() {
            const badge = document.getElementById('inventory-count-badge');
            if (!badge || !currentUser) return;
            const count = (currentUser.inventory || []).length;
            badge.innerText = count;
            badge.classList.toggle('hidden', count === 0);
        }

        function openInventoryModal() {
            const statusEl = document.getElementById('inventory-gift-status');
            if (statusEl) statusEl.classList.add('hidden');
            renderInventoryItems();
            document.getElementById('inventory-modal').classList.remove('hidden');
        }
        function closeInventoryModal() {
            document.getElementById('inventory-modal').classList.add('hidden');
        }

        function getNormalizedVipLabel(typeStr, fallbackName) {
            if (typeStr === 'vip_1d' || typeStr === '1d') return 'VIP 1 Ngày';
            if (typeStr === 'vip_30d' || typeStr === '30d') return 'VIP 1 Tháng';
            if (typeStr === 'vip_365d' || typeStr === '365d') return 'VIP 1 Năm';
            if (typeStr === 'vip_perm' || typeStr === 'perm') return 'VIP Vĩnh Viễn';
            return fallbackName || 'Gói VIP';
        }

        function renderInventoryItems() {
            const listEl = document.getElementById('inventory-list');
            if (!listEl || !currentUser) return;
            listEl.innerHTML = '';
            if (!currentUser.inventory || currentUser.inventory.length === 0) {
                listEl.innerHTML = `<div class="text-center py-8 text-xs text-slate-400">Túi đồ của bạn đang trống.</div>`;
                return;
            }

            const groupedMap = {};
            currentUser.inventory.forEach(item => {
                const key = item.type || item.name;
                if (!groupedMap[key]) {
                    groupedMap[key] = {
                        type: item.type,
                        name: getNormalizedVipLabel(item.type, item.name),
                        count: 0
                    };
                }
                groupedMap[key].count += 1;
            });

            Object.values(groupedMap).forEach(group => {
                const row = document.createElement('div');
                row.className = 'p-3 rounded-2xl bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 flex items-center justify-between gap-2';
                const countPrefix = group.count > 1 ? `<span class="px-1.5 py-0.5 rounded-md bg-amber-500 text-white text-[10px] font-black mr-1">x${group.count}</span>` : '';
                row.innerHTML = `
                    <div class="min-w-0">
                        <div class="font-extrabold text-xs text-slate-900 dark:text-white flex items-center truncate">
                            <i class="fa-solid fa-crown text-amber-500 mr-1.5"></i>${countPrefix}<span class="truncate">${group.name}</span>
                        </div>
                        <div class="text-[10px] text-slate-400">Số lượng: <b>x${group.count}</b></div>
                    </div>
                    <div class="flex items-center gap-1.5 flex-shrink-0">
                        <button type="button" onclick="useInventoryItemByType('${group.type}')" class="px-2.5 py-1.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs shadow-xs transition">Sử dụng</button>
                        <button type="button" onclick="openGiftModalForType('${group.type}', '${group.name}')" class="px-2.5 py-1.5 rounded-xl bg-gradient-to-r from-pink-500 to-rose-500 hover:from-pink-600 hover:to-rose-600 text-white font-bold text-xs shadow-xs transition"><i class="fa-solid fa-gift mr-1"></i>Gift</button>
                    </div>
                `;
                listEl.appendChild(row);
            });
        }

        function useInventoryItemByType(itemType) {
            if (!currentUser || !Array.isArray(currentUser.inventory)) return;
            const idx = currentUser.inventory.findIndex(i => (i.type || i.name) === itemType);
            if (idx === -1) return;
            const item = currentUser.inventory[idx];
            applyVipDurationToUser(currentUser, item.type);
            currentUser.inventory.splice(idx, 1);
            saveDatabases();
            initMainApp();
            renderInventoryItems();
            const statusEl = document.getElementById('inventory-gift-status');
            if (statusEl) {
                statusEl.innerText = `Đã kích hoạt sử dụng 1 ${getNormalizedVipLabel(item.type, item.name)}!`;
                statusEl.className = 'p-2.5 rounded-xl text-xs font-bold bg-emerald-500/10 text-emerald-500';
                statusEl.classList.remove('hidden');
            }
        }

        function openGiftModalForType(itemType, itemName) {
            pendingGiftItemType = itemType;
            pendingGiftItemName = itemName;
            document.getElementById('gift-item-name-display').innerText = itemName;
            document.getElementById('gift-recipient-input').value = '';
            document.getElementById('gift-input-error').classList.add('hidden');
            document.getElementById('inventory-modal').classList.add('hidden');
            document.getElementById('gift-input-modal').classList.remove('hidden');
        }

        function backToInventoryFromGift() {
            document.getElementById('gift-input-modal').classList.add('hidden');
            document.getElementById('inventory-modal').classList.remove('hidden');
        }

        function promptGiftConfirmation() {
            const rawRecipient = document.getElementById('gift-recipient-input').value.trim();
            const errEl = document.getElementById('gift-input-error');
            if (!rawRecipient) {
                errEl.innerText = 'Vui lòng nhập tên tài khoản người nhận!';
                errEl.classList.remove('hidden');
                return;
            }
            const targetKey = findExistingUserKey(rawRecipient);
            if (!targetKey || !usersDB[targetKey]) {
                errEl.innerText = `Tài khoản "${rawRecipient}" không tồn tại trong hệ thống!`;
                errEl.classList.remove('hidden');
                return;
            }
            if (currentUser && targetKey.toLowerCase() === currentUser.username.toLowerCase()) {
                errEl.innerText = 'Bạn không thể tự Gift cho chính mình!';
                errEl.classList.remove('hidden');
                return;
            }

            pendingGiftRecipientKey = targetKey;
            document.getElementById('gift-confirm-item-name').innerText = pendingGiftItemName;
            document.getElementById('gift-confirm-target-user').innerText = '@' + usersDB[targetKey].username;
            document.getElementById('gift-input-modal').classList.add('hidden');
            document.getElementById('gift-confirm-modal').classList.remove('hidden');
        }

        function cancelGiftConfirmation() {
            document.getElementById('gift-confirm-modal').classList.add('hidden');
            document.getElementById('gift-input-modal').classList.remove('hidden');
        }

        function executeGiftItem() {
            document.getElementById('gift-confirm-modal').classList.add('hidden');
            if (!currentUser || !pendingGiftItemType || !pendingGiftRecipientKey || !usersDB[pendingGiftRecipientKey]) {
                document.getElementById('inventory-modal').classList.remove('hidden');
                return;
            }

            const idx = currentUser.inventory.findIndex(i => (i.type || i.name) === pendingGiftItemType);
            if (idx === -1) {
                document.getElementById('inventory-modal').classList.remove('hidden');
                return;
            }

            const giftedItem = currentUser.inventory.splice(idx, 1)[0];
            if (!Array.isArray(usersDB[pendingGiftRecipientKey].inventory)) {
                usersDB[pendingGiftRecipientKey].inventory = [];
            }
            usersDB[pendingGiftRecipientKey].inventory.push({
                id: 'item_' + Date.now() + '_' + Math.random().toString(36).substring(2, 6),
                name: giftedItem.name,
                type: giftedItem.type,
                createdAt: Date.now()
            });

            saveDatabases();
            initMainApp();
            renderInventoryItems();
            document.getElementById('inventory-modal').classList.remove('hidden');

            const statusEl = document.getElementById('inventory-gift-status');
            if (statusEl) {
                statusEl.innerText = `Đã tặng thành công 1 ${pendingGiftItemName} cho @${usersDB[pendingGiftRecipientKey].username}!`;
                statusEl.className = 'p-2.5 rounded-xl text-xs font-bold bg-emerald-500/10 text-emerald-500';
                statusEl.classList.remove('hidden');
            }
        }

        function openRedeemModal() {
            document.getElementById('redeem-status-msg').classList.add('hidden');
            document.getElementById('redeem-code-input').value = '';
            document.getElementById('redeem-modal').classList.remove('hidden');
        }
        function closeRedeemModal() {
            document.getElementById('redeem-modal').classList.add('hidden');
        }

        function handleRedeemCode() {
            const raw = document.getElementById('redeem-code-input').value.trim().toUpperCase();
            const msgEl = document.getElementById('redeem-status-msg');
            if (!raw) return;
            const found = codesDB.find(c => c.code.toUpperCase() === raw);
            if (!found) {
                msgEl.innerText = 'Mã code không tồn tại hoặc đã bị xóa!';
                msgEl.className = 'p-3 rounded-xl text-xs font-bold bg-rose-500/10 text-rose-500';
                msgEl.classList.remove('hidden');
                return;
            }
            if (found.locked) {
                msgEl.innerText = 'Mã code này hiện đang bị KHÓA, không thể nhập!';
                msgEl.className = 'p-3 rounded-xl text-xs font-bold bg-amber-500/10 text-amber-500';
                msgEl.classList.remove('hidden');
                return;
            }
            if (found.usesLeft <= 0) {
                msgEl.innerText = 'Mã code này đã hết lượt sử dụng!';
                msgEl.className = 'p-3 rounded-xl text-xs font-bold bg-rose-500/10 text-rose-500';
                msgEl.classList.remove('hidden');
                return;
            }
            found.usesLeft -= 1;
            if (found.type === 'money') {
                currentUser.balance += Number(found.amount || 50000);
                msgEl.innerText = `Nhập code thành công! Bạn nhận được +${Number(found.amount || 50000).toLocaleString()} đ`;
            } else {
                applyVipDurationToUser(currentUser, found.type);
                msgEl.innerText = `Nhập code thành công! Đã kích hoạt gói VIP cho tài khoản của bạn!`;
            }
            msgEl.className = 'p-3 rounded-xl text-xs font-bold bg-emerald-500/10 text-emerald-500';
            msgEl.classList.remove('hidden');
            saveDatabases();
            initMainApp();
        }

        function openAdminModal() {
            if (!currentUser) return;
            const isAdmin = isAdminWebRole();
            const isMod = isModRole();
            const isVip = isVipRole();
            if (!isAdmin && !isMod && !isVip) return;

            // Role Mod TUYỆT ĐỐI KHÔNG THẤY Tab Cấp Role và Mật Khẩu
            document.getElementById('tab-btn-users').classList.toggle('hidden', isVip);
            document.getElementById('tab-btn-roles').classList.toggle('hidden', !isAdmin);
            document.getElementById('tab-btn-passwords').classList.toggle('hidden', !isAdmin);

            if (isVip && !isAdmin && !isMod) {
                ensureWeeklyVipCode(currentUser);
                document.getElementById('admin-modal-title').innerText = 'Đặc Quyền Role VIP Hàng Tuần';
                document.getElementById('admin-modal-subtitle').innerText = 'Nhận mã Code Premium 1 Ngày miễn phí mỗi tuần';
                switchAdminTab('codes');
            } else {
                document.getElementById('admin-modal-title').innerText = 'Bảng Quản Trị Hệ Thống';
                document.getElementById('admin-modal-subtitle').innerText = 'Quản lý thành viên, nạp/trừ tiền, cấp/xóa VIP và tạo mã code';
                switchAdminTab('users');
            }
            document.getElementById('admin-modal').classList.remove('hidden');
        }

        function closeAdminModal() {
            document.getElementById('admin-modal').classList.add('hidden');
        }

        function switchAdminTab(tabName) {
            const isAdmin = isAdminWebRole();
            if (!isAdmin && (tabName === 'roles' || tabName === 'passwords')) return;

            const tabs = ['users', 'codes', 'roles', 'passwords'];
            tabs.forEach(t => {
                const panel = document.getElementById('admin-tab-' + t);
                const btn = document.getElementById('tab-btn-' + t);
                if (panel) panel.classList.toggle('hidden', t !== tabName);
                if (btn) {
                    btn.className = (t === tabName)
                        ? 'py-2.5 px-3 rounded-2xl font-bold text-xs bg-indigo-600 text-white shadow-sm transition'
                        : 'py-2.5 px-3 rounded-2xl font-bold text-xs bg-slate-100 dark:bg-slate-800 text-slate-700 dark:text-slate-300 transition';
                }
            });

            if (tabName === 'users') loadNotebookUsers();
            if (tabName === 'codes') renderAdminCodesList();
            if (tabName === 'roles' && isAdmin) populateRoleTargetSelect();
            if (tabName === 'passwords' && isAdmin) renderAdminPasswordsGrid();
        }

        function toggleUserExpand(username) {
            if (expandedAdminUsers.has(username)) expandedAdminUsers.delete(username);
            else expandedAdminUsers.add(username);
            loadNotebookUsers();
        }

        function loadNotebookUsers() {
            const listEl = document.getElementById('admin-users-list');
            if (!listEl) return;
            const q = (document.getElementById('admin-user-search')?.value || '').toLowerCase().trim();
            listEl.innerHTML = '';

            const isAdmin = isAdminWebRole();
            const isMod = isModRole();

            Object.values(usersDB).forEach(u => {
                if (q && !u.username.toLowerCase().includes(q)) return;
                const isLocked = !isAdminWebRole(u) && u.lockedUntil && Date.now() < u.lockedUntil;
                const hasVip = isAdminWebRole(u) || isModRole(u) || isVipRole(u) || (u.activeVipUntil && Date.now() < u.activeVipUntil);
                const isExpanded = expandedAdminUsers.has(u.username);
                const allowLockThisUser = canUserLockTarget(currentUser, u);

                let buttonsInside = '';
                if (isAdmin) {
                    buttonsInside = `
                        <button type="button" onclick="adminAddMoneyModal('${u.username}')" class="px-2.5 py-1.5 rounded-lg bg-emerald-600 hover:bg-emerald-700 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs">+ Tiền</button>
                        <button type="button" onclick="adminSubtractMoneyModal('${u.username}')" class="px-2.5 py-1.5 rounded-lg bg-orange-600 hover:bg-orange-700 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs">- Trừ Tiền</button>
                        <button type="button" onclick="adminManageVipModal('${u.username}')" class="px-2.5 py-1.5 rounded-lg bg-amber-600 hover:bg-amber-700 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs">Cấp VIP</button>
                        <button type="button" onclick="adminRemoveVipAction('${u.username}')" class="px-2.5 py-1.5 rounded-lg bg-rose-600 hover:bg-rose-700 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs">Xóa VIP</button>
                        ${allowLockThisUser
                            ? (isLocked
                                ? `<button type="button" onclick="adminUnlockAccount('${u.username}')" class="px-2.5 py-1.5 rounded-lg bg-cyan-600 hover:bg-cyan-700 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs">Mở khóa</button>`
                                : `<button type="button" onclick="adminOpenLockModal('${u.username}')" class="px-2.5 py-1.5 rounded-lg bg-rose-700 hover:bg-rose-800 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs">Khóa acc</button>`)
                            : `<span class="px-2 py-1 rounded-lg bg-slate-200 dark:bg-slate-800 text-slate-500 text-[10px] font-bold">Không thể khóa Admin Web</span>`
                        }
                    `;
                } else if (isMod) {
                    buttonsInside = `
                        <button type="button" onclick="adminManageVipModal('${u.username}')" class="px-3 py-1.5 rounded-lg bg-amber-600 hover:bg-amber-700 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs"><i class="fa-solid fa-crown mr-1"></i>Cấp VIP</button>
                        <button type="button" onclick="adminRemoveVipAction('${u.username}')" class="px-3 py-1.5 rounded-lg bg-rose-600 hover:bg-rose-700 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs">Xóa VIP</button>
                        ${allowLockThisUser ? (isLocked ? `<button type="button" onclick="adminUnlockAccount('${u.username}')" class="px-3 py-1.5 rounded-lg bg-cyan-600 hover:bg-cyan-700 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs"><i class="fa-solid fa-lock-open mr-1"></i>Mở khóa</button>` : `<button type="button" onclick="adminOpenLockModal('${u.username}')" class="px-3 py-1.5 rounded-lg bg-rose-700 hover:bg-rose-800 text-white text-[11px] font-bold flex items-center gap-1 shadow-xs"><i class="fa-solid fa-user-lock mr-1"></i>Khóa acc</button>`) : `<span class="px-2 py-1 rounded-lg bg-slate-200 dark:bg-slate-800 text-slate-500 text-[10px] font-bold">Không thể khóa Admin/Mod</span>`}
                    `;
                }

                const card = document.createElement('div');
                card.className = 'p-3.5 rounded-2xl bg-slate-50 dark:bg-slate-800/70 border border-slate-200 dark:border-slate-800 space-y-2';
                card.innerHTML = `
                    <div class="flex items-center justify-between">
                        <div class="flex items-center gap-2.5">
                            <div class="w-9 h-9 rounded-xl bg-indigo-600 text-white font-bold text-xs flex items-center justify-center">${u.username.charAt(0).toUpperCase()}</div>
                            <div>
                                <div class="font-extrabold text-xs text-slate-900 dark:text-white flex items-center gap-1.5">
                                    ${u.username}
                                    <span class="px-2 py-0.5 rounded-md bg-indigo-500/10 text-indigo-600 dark:text-indigo-400 text-[10px] font-extrabold uppercase">${u.role || 'member'}</span>
                                    ${hasVip ? '<span class="px-1.5 py-0.5 rounded bg-amber-500/20 text-amber-500 text-[10px] font-extrabold">VIP</span>' : ''}
                                    ${isLocked ? '<span class="px-1.5 py-0.5 rounded bg-rose-500 text-white text-[10px] font-extrabold">ĐANG KHÓA</span>' : ''}
                                </div>
                                <div class="text-[11px] text-slate-500">Số dư: <b class="text-indigo-600 dark:text-indigo-400">${formatUserBalance(u)}</b></div>
                            </div>
                        </div>
                        <button type="button" onclick="toggleUserExpand('${u.username}')" class="px-3 py-1.5 rounded-xl bg-indigo-600 hover:bg-indigo-700 text-white font-bold text-xs">
                            Quản lý <i class="fa-solid fa-chevron-${isExpanded ? 'up' : 'down'} ml-1 text-[10px]"></i>
                        </button>
                    </div>
                    <div class="${isExpanded ? 'flex' : 'hidden'} items-center gap-1.5 pt-2 flex-wrap border-t border-slate-200 dark:border-slate-700">
                        ${buttonsInside}
                    </div>
                `;
                listEl.appendChild(card);
            });
        }

        function adminAddMoneyModal(username) {
            pendingMoneyTarget = username;
            pendingMoneyMode = 'add';
            document.getElementById('money-modal-title').innerText = `Cộng tiền cho @${username}`;
            document.getElementById('money-modal').classList.remove('hidden');
        }

        function adminSubtractMoneyModal(username) {
            pendingMoneyTarget = username;
            pendingMoneyMode = 'sub';
            document.getElementById('money-modal-title').innerText = `Trừ tiền của @${username}`;
            document.getElementById('money-modal').classList.remove('hidden');
        }

        function confirmMoneyAction() {
            const amount = Number(document.getElementById('money-modal-input').value || 0);
            if (pendingMoneyTarget && usersDB[pendingMoneyTarget] && amount > 0) {
                if (!isAdminWebRole(usersDB[pendingMoneyTarget])) {
                    if (pendingMoneyMode === 'add') usersDB[pendingMoneyTarget].balance = (usersDB[pendingMoneyTarget].balance || 0) + amount;
                    else usersDB[pendingMoneyTarget].balance = Math.max(0, (usersDB[pendingMoneyTarget].balance || 0) - amount);
                }
                saveDatabases();
                initMainApp();
                loadNotebookUsers();
            }
            document.getElementById('money-modal').classList.add('hidden');
        }

        function adminManageVipModal(username) {
            pendingVipTarget = username;
            document.getElementById('admin-vip-modal').classList.remove('hidden');
        }

        function confirmAdminGrantVip() {
            const dur = document.getElementById('admin-vip-duration').value;
            if (pendingVipTarget && usersDB[pendingVipTarget]) {
                applyVipDurationToUser(usersDB[pendingVipTarget], dur);
                saveDatabases();
                initMainApp();
                loadNotebookUsers();
            }
            document.getElementById('admin-vip-modal').classList.add('hidden');
        }

        function adminRemoveVipAction(username) {
            if (usersDB[username]) {
                usersDB[username].activeVipUntil = 0;
                saveDatabases();
                initMainApp();
                loadNotebookUsers();
            }
        }

        function adminOpenLockModal(username) {
            if (!usersDB[username] || !canUserLockTarget(currentUser, usersDB[username])) return;
            pendingLockTarget = username;
            document.getElementById('lock-choice-modal').classList.remove('hidden');
        }

        function promptLockConfirmation() {
            const radios = document.getElementsByName('lock_time_choice');
            for (let r of radios) {
                if (r.checked) pendingLockDuration = r.value;
            }
            document.getElementById('lock-choice-modal').classList.add('hidden');
            document.getElementById('lock-confirm-modal').classList.remove('hidden');
        }

        function executeLockAccount() {
            document.getElementById('lock-confirm-modal').classList.add('hidden');
            if (!pendingLockTarget || !usersDB[pendingLockTarget]) return;
            if (!canUserLockTarget(currentUser, usersDB[pendingLockTarget])) return;
            let durMs = 15 * 60 * 1000;
            if (pendingLockDuration === '1h') durMs = 3600 * 1000;
            else if (pendingLockDuration === '1d') durMs = 24 * 3600 * 1000;
            else if (pendingLockDuration === '7d') durMs = 7 * 24 * 3600 * 1000;
            else if (pendingLockDuration === '30d') durMs = 30 * 24 * 3600 * 1000;
            else if (pendingLockDuration === 'perm') durMs = 36500 * 24 * 3600 * 1000;

            usersDB[pendingLockTarget].lockedUntil = Date.now() + durMs;
            saveDatabases();
            loadNotebookUsers();
        }

        function adminUnlockAccount(username) {
            if (!usersDB[username] || !canUserLockTarget(currentUser, usersDB[username])) return;
            usersDB[username].lockedUntil = 0;
            saveDatabases();
            loadNotebookUsers();
        }

        function toggleCodeAmountInput() {
            const type = document.getElementById('new-code-type').value;
            document.getElementById('new-code-amount').classList.toggle('hidden', type !== 'money');
        }

        function generateRandomCode11To19() {
            const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
            const len = Math.floor(Math.random() * 9) + 11;
            let res = '';
            for (let i = 0; i < len; i++) {
                res += chars.charAt(Math.floor(Math.random() * chars.length));
            }
            return res;
        }

        function adminCreateCode() {
            if (!isAdminWebRole() && !isModRole()) return;
            let rawCode = document.getElementById('new-code-str').value.trim().toUpperCase();
            if (!rawCode) {
                rawCode = generateRandomCode11To19();
            }
            const type = document.getElementById('new-code-type').value;
            const amount = Number(document.getElementById('new-code-amount').value || 50000);
            const usesLeft = Number(document.getElementById('new-code-uses').value || 1);

            codesDB.unshift({
                code: rawCode,
                type: type,
                amount: amount,
                usesLeft: usesLeft,
                locked: false
            });
            document.getElementById('new-code-str').value = '';
            saveDatabases();
            renderAdminCodesList();
        }

        function renderAdminCodesList() {
            const isVipOnly = isVipRole() && !isAdminWebRole() && !isModRole();
            document.getElementById('vip-weekly-only-box').classList.toggle('hidden', !isVipOnly);
            document.getElementById('admin-code-creator-box').classList.toggle('hidden', isVipOnly);
            const listEl = document.getElementById('admin-codes-list');
            listEl.innerHTML = '';

            if (isVipOnly) {
                ensureWeeklyVipCode(currentUser);
                document.getElementById('vip-weekly-code-display').innerText = currentUser.weeklyVipCode || '---';
                return;
            }

            if (codesDB.length === 0) {
                listEl.innerHTML = `<div class="text-center py-4 text-xs text-slate-400">Chưa có mã code nào.</div>`;
                return;
            }

            codesDB.forEach((c, idx) => {
                const row = document.createElement('div');
                row.className = 'p-3 rounded-2xl bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 flex flex-wrap items-center justify-between gap-2';
                const rewardLabel = c.type === 'money' ? `${Number(c.amount || 0).toLocaleString()} đ` : c.type.toUpperCase();
                row.innerHTML = `
                    <div>
                        <div class="font-mono font-extrabold text-xs text-indigo-600 dark:text-indigo-400 flex items-center gap-2">
                            ${c.code}
                            ${c.locked ? '<span class="px-1.5 py-0.5 rounded bg-rose-500 text-white text-[10px]">Đang Khóa</span>' : '<span class="px-1.5 py-0.5 rounded bg-emerald-500/10 text-emerald-500 text-[10px]">Hoạt động</span>'}
                        </div>
                        <div class="text-[11px] text-slate-500">Thưởng: <b>${rewardLabel}</b> • Còn lại: <b>${c.usesLeft} lượt</b></div>
                    </div>
                    <div class="flex items-center gap-1.5">
                        <button onclick="copySingleCode('${c.code}')" class="px-2.5 py-1 rounded-lg bg-slate-200 dark:bg-slate-700 text-xs font-bold">Chép</button>
                        ${c.locked
                            ? `<button onclick="toggleLockCode(${idx}, false)" class="px-2.5 py-1 rounded-lg bg-emerald-600 text-white text-xs font-bold">Mở code</button>`
                            : `<button onclick="toggleLockCode(${idx}, true)" class="px-2.5 py-1 rounded-lg bg-amber-500 text-white text-xs font-bold">Khóa code</button>`
                        }
                        <button onclick="deleteCodeItem(${idx})" class="px-2.5 py-1 rounded-lg bg-rose-600 text-white text-xs font-bold">Xóa code</button>
                    </div>
                `;
                listEl.appendChild(row);
            });
        }

        function copyWeeklyVipCode() {
            if (!currentUser || !currentUser.weeklyVipCode) return;
            copySingleCode(currentUser.weeklyVipCode);
        }

        function copySingleCode(str) {
            const ta = document.createElement('textarea');
            ta.value = str;
            document.body.appendChild(ta);
            ta.select();
            document.execCommand('copy');
            document.body.removeChild(ta);
        }

        function toggleLockCode(idx, lockState) {
            if (codesDB[idx]) {
                codesDB[idx].locked = lockState;
                saveDatabases();
                renderAdminCodesList();
            }
        }

        function deleteCodeItem(idx) {
            codesDB.splice(idx, 1);
            saveDatabases();
            renderAdminCodesList();
        }

        function populateRoleTargetSelect() {
            const sel = document.getElementById('role-target-username');
            if (!sel) return;
            sel.innerHTML = '';
            Object.values(usersDB).forEach(u => {
                if (u.username.toLowerCase() === 'henhenbak') return;
                const opt = document.createElement('option');
                opt.value = u.username;
                opt.innerText = `${u.username} (Hiện tại: ${u.role || 'member'})`;
                sel.appendChild(opt);
            });
        }

        function selectRoleButton(roleType) {
            selectedRoleChoice = roleType;
            const map = {
                'admin web': 'role-btn-admin',
                'mod': 'role-btn-mod',
                'vip': 'role-btn-vip',
                'member': 'role-btn-member',
                'custom': 'role-btn-custom'
            };
            Object.keys(map).forEach(k => {
                const btn = document.getElementById(map[k]);
                if (btn) {
                    btn.className = (k === roleType)
                        ? 'py-2.5 px-2 rounded-xl border-2 border-indigo-600 bg-indigo-600 text-white font-bold text-xs'
                        : 'py-2.5 px-2 rounded-xl border border-slate-300 dark:border-slate-700 bg-white dark:bg-slate-900 font-bold text-xs';
                }
            });
            document.getElementById('custom-role-input-box').classList.toggle('hidden', roleType !== 'custom');
        }

        function getNextNumberedRoleName(baseRole) {
            const existing = Object.values(usersDB).filter(u => getBaseRole(u.role) === baseRole);
            if (existing.length === 0) return baseRole;
            return `${baseRole} ${existing.length + 1}`;
        }

        function showRoleAlert(msg, isSuccess) {
            const el = document.getElementById('role-status-alert');
            el.innerText = msg;
            el.className = `p-2.5 rounded-xl text-xs font-bold ${isSuccess ? 'bg-emerald-500/10 text-emerald-500' : 'bg-rose-500/10 text-rose-500'}`;
            el.classList.remove('hidden');
        }

        function executeAssignRole() {
            if (!isAdminWebRole()) return;
            const targetName = document.getElementById('role-target-username').value;
            if (!targetName || !usersDB[targetName]) return;
            const targetUser = usersDB[targetName];

            if (targetUser.username.toLowerCase() === 'henhenbak') {
                return showRoleAlert('Không thể thay đổi quyền của tài khoản chủ web gốc!', false);
            }

            let finalRole = selectedRoleChoice;
            if (selectedRoleChoice === 'custom') {
                const customInput = document.getElementById('custom-role-name-input').value.trim();
                if (!customInput) return showRoleAlert('Vui lòng nhập tên Role tùy chỉnh muốn cấp!', false);
                finalRole = customInput;
            } else if (selectedRoleChoice === 'admin web' || selectedRoleChoice === 'mod') {
                finalRole = getNextNumberedRoleName(selectedRoleChoice);
            }

            targetUser.role = finalRole;
            if (isAdminWebRole(targetUser)) {
                targetUser.lockedUntil = 0;
                targetUser.balance = 999999;
            }
            if (selectedRoleChoice === 'vip') ensureWeeklyVipCode(targetUser);
            saveDatabases();
            initMainApp();
            populateRoleTargetSelect();
            loadNotebookUsers();
            showRoleAlert(`Đã cấp role "${finalRole}" cho tài khoản @${targetName}!`, true);
        }

        function executeRemoveRole() {
            if (!isAdminWebRole()) return;
            const targetName = document.getElementById('role-target-username').value;
            if (!targetName || !usersDB[targetName]) return;
            const targetUser = usersDB[targetName];

            if (targetUser.username.toLowerCase() === 'henhenbak') {
                return showRoleAlert('Không thể xóa role của tài khoản chủ web gốc!', false);
            }

            // CHỈ HENHENBAK MỚI ĐƯỢC XÓA HOẶC ĐỔI ROLE CỦA CÁC ADMIN WEB KHÁC (ADMIN 2, ADMIN 3...)
            if (isAdminWebRole(targetUser) && currentUser.username.toLowerCase() !== 'henhenbak') {
                return showRoleAlert('Chỉ có tài khoản chủ web gốc "henhenbak" mới có quyền xóa hoặc thay đổi role của các tài khoản Admin Web khác!', false);
            }

            targetUser.role = 'member';
            saveDatabases();
            populateRoleTargetSelect();
            loadNotebookUsers();
            showRoleAlert(`Đã xóa role của @${targetName} về lại member!`, true);
        }

        function renderAdminPasswordsGrid() {
            if (!isAdminWebRole()) return;
            const grid = document.getElementById('admin-passwords-grid');
            if (!grid) return;
            grid.innerHTML = '';
            Object.values(usersDB).forEach(u => {
                const card = document.createElement('div');
                card.className = 'p-3.5 rounded-2xl bg-slate-50 dark:bg-slate-800 border border-slate-200 dark:border-slate-700 flex items-center justify-between';
                card.innerHTML = `
                    <div>
                        <div class="font-extrabold text-xs text-slate-900 dark:text-white">@${u.username} <span class="text-[10px] text-indigo-500 uppercase">(${u.role || 'member'})</span></div>
                        <div class="text-xs text-slate-500 mt-0.5">Mật khẩu: <b class="font-mono text-rose-500 select-all">${u.password}</b></div>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        window.addEventListener('DOMContentLoaded', async () => {
            loadLocalDatabasesImmediate();
            loadRememberedCredentials();
            renderCurrentMessages();
            if (window.cloudLoad) {
                const cloudData = await window.cloudLoad();
                if (cloudData && cloudData.users && Object.keys(cloudData.users).length > 0) {
                    usersDB = { ...usersDB, ...cloudData.users };
                    if (Array.isArray(cloudData.codes) && cloudData.codes.length > 0) {
                        codesDB = cloudData.codes;
                    }
                    ensureDefaultAdminAccount();
                }
            }
        });
    </script>
</body>
</html>