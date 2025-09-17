
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>奇美醫院品質提升活動儀表板</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f3f4f6;
            color: #1f2937;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }
        .card {
            border-radius: 1rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 1.5rem;
            margin-bottom: 2rem;
        }
        .section-title {
            font-size: 1.5rem;
            font-weight: bold;
            color: #111827;
            margin-bottom: 1rem;
        }
        .progress-bar {
            height: 0.75rem;
            border-radius: 9999px;
            background-color: #e5e7eb;
            overflow: hidden;
        }
        .progress-fill {
            height: 100%;
            transition: width 0.5s ease-in-out;
            border-radius: 9999px;
        }
        .task-list li {
            padding: 0.75rem 0;
            border-bottom: 1px solid #e5e7eb;
        }
        .task-list li:last-child {
            border-bottom: none;
        }
        .status-badge {
            display: inline-block;
            padding: 0.25rem 0.75rem;
            border-radius: 9999px;
            font-size: 0.875rem;
            font-weight: 500;
        }
        .status-completed {
            background-color: #d1fae5;
            color: #065f46;
        }
        .status-upcoming {
            background-color: #e0f2fe;
            color: #0c4a6e;
        }
        .status-inprogress {
            background-color: #fef9c3;
            color: #854d0e;
        }
        .status-award {
            background-color: #ffedd5;
            color: #9a3412;
        }
        .status-promoted {
            background-color: #dbeafe;
            color: #1e40af;
        }
        .tab-button {
            padding: 0.75rem 1.5rem;
            font-size: 1.125rem;
            font-weight: 500;
            color: #6b7280;
            border-bottom: 3px solid transparent;
            cursor: pointer;
            transition: all 0.2s ease-in-out;
        }
        .tab-button:hover {
            color: #4b5563;
        }
        .tab-button.active {
            color: #111827;
            border-color: #2563eb;
        }
        .sub-tab-button {
            padding: 0.5rem 1rem;
            font-size: 1rem;
            font-weight: 500;
            color: #6b7280;
            border-radius: 0.5rem;
            cursor: pointer;
            transition: all 0.2s ease-in-out;
            background-color: transparent;
        }
        .sub-tab-button:hover {
            background-color: #e5e7eb;
        }
        .sub-tab-button.active {
            background-color: #d1fae5;
            color: #065f46;
        }
        /* Custom background colors */
        .bg-white-card {
            background-color: #ffffff;
        }
        .bg-pink-card {
            background-color: #fce7f3;
        }
        .bg-yellow-card {
            background-color: #fffbeb;
        }
        .month-title {
            background-color: #d1fae5;
            color: #065f46;
            padding: 0.5rem 1rem;
            border-radius: 0.5rem;
            font-weight: bold;
            font-size: 1.25rem;
            margin-bottom: 0.75rem;
        }
    </style>
</head>
<body class="bg-gray-100 p-8">
    <div class="container">
        <header class="text-center mb-8">
            <h1 class="text-4xl font-extrabold text-gray-900 mb-2">奇美醫院品質提升活動儀表板</h1>
            <p class="text-xl text-gray-600">追蹤所有院內外品質活動的進度</p>
        </header>

        <!-- Tab Buttons -->
        <div class="flex justify-center mb-8 border-b border-gray-300">
            <button class="tab-button active" data-tab="internal">院內品質提升活動</button>
            <button class="tab-button" data-tab="external">院外品質競賽</button>
        </div>

        <!-- Tab Content -->
        <div id="internal-tab" class="tab-content active">
            <section id="internal-section" class="card bg-white">
                <h2 class="section-title">院內品質提升活動</h2>
                <!-- Internal Sub-tab Buttons -->
                <div class="flex flex-wrap gap-2 mb-6" id="internal-sub-tabs">
                    <button class="sub-tab-button active" data-category="qccTeam">QCC團隊</button>
                    <button class="sub-tab-button" data-category="qmConsultants">品管輔導員</button>
                    <button class="sub-tab-button" data-category="allHospitalEvents">全院性活動</button>
                </div>
                <div id="internal-projects" class="space-y-6"></div>
            </section>
        </div>

        <div id="external-tab" class="tab-content hidden">
            <section id="external-section" class="card bg-white">
                <div class="flex items-center justify-between mb-4">
                    <h2 class="section-title" id="external-title">所有競賽</h2>
                </div>
                <!-- Sub-tab Buttons -->
                <div class="flex flex-wrap gap-2 mb-6" id="external-sub-tabs"></div>
                <!-- Sub-tab Content -->
                <div id="external-projects" class="space-y-6"></div>
            </section>
        </div>

        <footer class="text-center text-gray-500 mt-8">
            <p>&copy; 2025 奇美醫院品質管理部. All rights reserved.</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const externalProjectsData = {
                '醫策會-國家醫療品質獎(NHQA)': {
                    '主題類': [
                        {
                            name: '主題改善組/菁英組',
                            team: '改善組:ICG圈, 菁英組:藥帶圈、急品圈安老組、救生圈',
                            progress: 80,
                            tasks: [
                                { description: '5/9(五) 前繳交競賽書面資料+報名表', status: 'completed' },
                                { description: '6-7月 報名資料行政審查及書面審查', status: 'completed' },
                                { description: '8/5(二) ICG圈面談', status: 'completed' },
                                { description: '9/11(四) 急品圈安老組實審', status: 'inprogress' },
                                { description: '9/23(二) 藥帶圈實審', status: 'inprogress' },
                                { description: '9/25(四) 救生圈實審', status: 'inprogress' },
                                { description: '10/27-11/7 現場發表', status: 'upcoming' },
                                { description: '12月 頒獎典禮', status: 'upcoming' },
                                { description: '進級狀況: ICG圈、藥帶圈、急品圈安老組、救生圈 晉級', status: 'promoted' }
                            ]
                        },
                    ],
                    '系統類': [
                        {
                            name: '系統類',
                            team: '卓越中心:藥劑部',
                            progress: 70,
                            tasks: [
                                { description: '5/29(四) 前繳交書面資料+完成報名', status: 'completed' },
                                { description: '6-7月 書面審查', status: 'completed' },
                                { description: '10/15(三) 實地審查', status: 'upcoming' },
                                { description: '12月 頒獎典禮', status: 'upcoming' }
                            ]
                        }
                    ],
                    '傑出醫療類': [
                        {
                            name: '傑出醫療類',
                            team: '放射腫瘤部、預防醫學科',
                            progress: 50,
                            tasks: [
                                { description: '5/29(四) 前繳交書面資料+完成報名', status: 'completed' },
                                { description: '6-7月 書面審查', status: 'completed' },
                                { description: '11/11(二) 放射腫瘤部實地審查', status: 'upcoming' },
                                { description: '11/28(五) 預防醫學科實地審查', status: 'upcoming' },
                                { description: '12月 頒獎典禮', status: 'upcoming' }
                            ]
                        }
                    ],
                    '智慧醫療類': [
                        {
                            name: '智慧醫療類',
                            team: '智慧解決方案組:18組, 智慧服務組:2組(門、急診服務流程)',
                            progress: 70,
                            tasks: [
                                { description: '5/29(四) 前繳交書面資料+完成報名', status: 'completed' },
                                { description: '6-7月 書面審查', status: 'completed' },
                                { description: '9/1(一)-9/12(五) 解決方案組現場發表', status: 'inprogress' },
                                { description: '10/21(二) 服務流程組實地審查', status: 'upcoming' },
                                { description: '11月 解決方案組/服務流程組現場發表', status: 'upcoming' },
                                { description: '11月 解決方案組實地審查', status: 'upcoming' },
                                { description: '12月 頒獎典禮', status: 'upcoming' },
                                { description: '進級狀況: 解決方案組18組、服務流程組2組 晉級', status: 'promoted' }
                            ]
                        }
                    ],
                    '淨零醫療類': [
                        {
                            name: '淨零醫療類',
                            team: '(企管部主責招募) 今年規劃,明年參賽',
                            progress: 0,
                            tasks: [
                                { description: '無時程規劃', status: 'upcoming' }
                            ]
                        }
                    ]
                },
                '台灣醫務管理學會': [
                    {
                        name: '台灣健康照護品質管理競賽',
                        team: '救生圈、急品圈安老組、強心圈、救腦圈、綠巨人圈、足穩圈、是8Life',
                        progress: 90,
                        tasks: [
                            { description: '5/7(三) 前繳交競賽書面資料+報名表', status: 'completed' },
                            { description: '7/2(三) 公告書審結果', status: 'completed' },
                            { description: '7/25(五) 前報名決賽+繳費', status: 'completed' },
                            { description: '8/7(四) 決賽發表', status: 'completed' },
                            { description: '10/14(二) 頒獎典禮', status: 'upcoming' },
                            { description: '獲獎狀況: 2銅、4佳作、1入選', status: 'award' }
                        ]
                    }
                ],
                '財團法人先鋒品質管制學術研究基金會': [
                    {
                        name: '全國品管圈大會',
                        team: '受益圈',
                        progress: 90,
                        tasks: [
                            { description: '3/28(五) 前繳交報名申請', status: 'completed' },
                            { description: '5/2(五) 前繳交書面資料', status: 'completed' },
                            { description: '6/20(五) 發表會', status: 'completed' },
                            { description: '8/21(四) 總會決賽-實地審查', status: 'completed' },
                            { description: '11/10(一)-11/14(五) 總會決賽-發表暨頒獎', status: 'upcoming' },
                            { description: '獲獎狀況: 特優獎、全國潛力圈長獎', status: 'award' }
                        ]
                    },
                    {
                        name: '國際品管圈大會(ICQCC)',
                        team: '救生圈、足穩圈',
                        progress: 70,
                        tasks: [
                            { description: '4/30(三) 前完成報名+書面資料', status: 'completed' },
                            { description: '6/3(二) 前繳交中英文摘要', status: 'completed' },
                            { description: '7/25(五) 英文書面資料+PPT', status: 'completed' },
                            { description: '11/3(一)-11/5(三) 發表大會', status: 'upcoming' },
                            { description: '進級狀況: 2組 通過', status: 'promoted' }
                        ]
                    }
                ],
                '中衛發展中心': [
                    {
                        name: '臺灣持續改善案例競賽',
                        team: '藥帶圈、受益圈、急品圈安老組、ICG圈、救生圈',
                        progress: 50,
                        tasks: [
                            { description: '4/30(三)前完成登錄報名', status: 'completed' },
                            { description: '5/16(五)前繳交書面資料', status: 'completed' },
                            { description: '6/12(四)區會初賽-南區發表會', status: 'completed' },
                            { description: '6/13(五)南區頒獎典禮', status: 'completed' },
                            { description: '8/21(四)下午-受益圈 總會決賽-實地審查', status: 'completed' },
                            { description: '8/29(五)上午-ICG圈、下午-救生圈 總會決賽-實地審查', status: 'completed' },
                            { description: '9/24(三)上午-急品圈安老組 總會決賽-實地審查', status: 'inprogress' },
                            { description: '10/2(四)上午-藥帶圈 總會決賽-實地審查', status: 'upcoming' },
                            { description: '11/10(一)-11/14(五)總會決賽-發表暨頒獎', status: 'upcoming' }
                        ]
                    }
                ],
                '台灣醫療品質協會': [
                    {
                        name: '品質改善成果發表競賽',
                        team: '招募中',
                        progress: 50,
                        tasks: [
                            { description: '9/25(四)前繳交競賽報名表+書面資料', status: 'inprogress' },
                            { description: '10/3(五)前完成報名及寄資料', status: 'upcoming' },
                            { description: '11/3(一)一階-書面審查', status: 'upcoming' },
                            { description: '12/12(五)二階-發表/頒獎', status: 'upcoming' }
                        ]
                    }
                ],
                '生策中心': [
                    {
                        name: '國家品質標章暨國家生技醫療品質獎(SNQ)',
                        team: 'SNQ續審12件、新申請3件',
                        progress: 50,
                        tasks: [
                            { description: '7/31 前完成報名及繳交書面資料', status: 'completed' },
                            { description: '9/30(二)前送出續審申請資料', status: 'inprogress' },
                            { description: '10/3、10/7、10/16 複審-簡報審查', status: 'upcoming' },
                            { description: '10月下旬-11月上旬 決審-實地勘查', status: 'upcoming' },
                            { description: '結果公告及頒獎', status: 'upcoming' }
                        ]
                    }
                ]
            };
            
            const internalProjectsData = {
                'qccTeam': {
                    name: '品質提升活動年計畫-QCC團隊',
                    backgroundClass: 'bg-white-card',
                    months: {
                        '2月': [
                            { date: '2/12(三)', description: '品質提升活動 QCC 運作說明會', status: 'completed' },
                            { date: '2/25(二)', description: '品質提升活動課程(Q1)', status: 'completed' }
                        ],
                        '3月': [
                            { date: '3/5(三) & 3/6(四)', description: '進度輔導(Q2)', status: 'completed' },
                            { date: '3/20(四)', description: '品質提升活動課程(Q3)', status: 'completed' }
                        ],
                        '4月': [
                             { date: '4/17(四) & 4/21(一)', description: '進度輔導(Q5)', status: 'completed' },
                             { date: '4/21(一)', description: '品質提升活動課程(Q4)', status: 'completed' }
                        ],
                        '6月': [
                            { date: '6/9(一) & 6/12(四)', description: '進度輔導(Q6)', status: 'completed' }
                        ],
                        '7月': [
                            { date: '7/17(四)', description: '品質提升活動期中發表會', status: 'completed' },
                            { date: '7/31(四) & 8/14(四)', description: '進度輔導(Q7)', status: 'completed' }
                        ],
                        '8月': [
                            { date: '8/21(四) & 8/22(五)', description: '品質提升活動課程(Q8)', status: 'completed' }
                        ],
                        '10月': [
                            { date: '10/15(三) & 10/16(四)', description: '進度輔導(Q10)', status: 'upcoming' }
                        ],
                        '12月': [
                            { date: '12/11(四) & 12/18(四)', description: '進度輔導(Q11)', status: 'upcoming' }
                        ],
                        '隔年2月': [
                            { date: '2/11(三)-2/12(四)', description: '品質提升活動期末成果發表會', status: 'upcoming' }
                        ]
                    }
                },
                'qmConsultants': {
                    name: '品管輔導員',
                    backgroundClass: 'bg-white-card',
                    months: {
                        '3月': [
                            { date: '3/21(五)', description: '品管輔導員交流共識會', status: 'completed' }
                        ],
                        '6月': [
                            { date: '6/26(四)', description: '品管輔導員培訓課程－書面資料審閱技巧實戰', status: 'completed' }
                        ]
                    }
                },
                'allHospitalEvents': {
                    name: '全院性活動',
                    backgroundClass: 'bg-white-card',
                    months: {
                        '2月': [
                            { date: '2/12(三)', description: '品質提升活動 QCC 運作說明會', status: 'completed' },
                            { date: '2/25(二)', description: '品質提升活動課程(Q1)', status: 'completed' }
                        ],
                        '3月': [
                            { date: '3/20(四)', description: '品管通識課程-多元品管手法及工具簡介', status: 'completed' }
                        ],
                        '6月': [
                             { date: '6/26(四)', description: '醫品圈標竿學習發表會', status: 'completed' }
                        ],
                        '隔年2月': [
                            { date: '2/11(三)-2/12(四)', description: '品質提升活動期末成果發表會', status: 'upcoming' }
                        ]
                    }
                }
            };
            
            const renderInternalProjects = (category) => {
                const container = document.getElementById('internal-projects');
                container.innerHTML = ''; 
                const projectData = internalProjectsData[category];
                if (!projectData) {
                    container.innerHTML = `<p class="text-gray-500 text-center">目前無相關活動。</p>`;
                    return;
                }

                const cardHtml = `
                    <div class="p-6 rounded-xl shadow-sm ${projectData.backgroundClass}">
                        <h3 class="font-bold text-lg mb-4">${projectData.name}</h3>
                        ${Object.keys(projectData.months).map(month => `
                            <div class="mb-4">
                                <h4 class="month-title">${month}</h4>
                                <ul class="task-list">
                                    ${projectData.months[month].map(task => `
                                        <li>
                                            <div class="flex items-center justify-between">
                                                <span>${task.description} <span class="text-gray-500 text-sm">(${task.date})</span></span>
                                                <span class="status-badge ${getStatusBadgeClass(task.status)}">${getStatusText(task.status)}</span>
                                            </div>
                                        </li>
                                    `).join('')}
                                </ul>
                            </div>
                        `).join('')}
                    </div>
                `;
                container.innerHTML += cardHtml;
            };

            const renderExternalProjects = (organizer, subCategory = null) => {
                const container = document.getElementById('external-projects');
                container.innerHTML = '';
                let projectsToRender = [];

                if (organizer === 'upcoming') {
                    const upcomingTasks = [];
                    const today = new Date();
                    const currentMonth = today.getMonth() + 1;

                    const traverseData = (data, organizerName = null) => {
                        for (const key in data) {
                            const projects = data[key];
                            if (Array.isArray(projects)) {
                                projects.forEach(project => {
                                    project.tasks.forEach(task => {
                                        const taskDateMatch = task.description.match(/(\d{1,2})\/(\d{1,2})/);
                                        const taskMonth = taskDateMatch ? parseInt(taskDateMatch[1], 10) : null;
                                        
                                        const isUpcoming = task.status === 'upcoming';
                                        const isInprogress = task.status === 'inprogress';
                                        
                                        if ((isUpcoming || isInprogress) && taskMonth >= currentMonth && taskMonth <= 12) {
                                            upcomingTasks.push({
                                                organizer: organizerName || key,
                                                projectName: project.name,
                                                task: task
                                            });
                                        }
                                    });
                                });
                            } else if (typeof projects === 'object') {
                                traverseData(projects, key);
                            }
                        }
                    };
                    traverseData(externalProjectsData);
                    projectsToRender = upcomingTasks.map(item => ({
                        name: `${item.organizer} - ${item.projectName}`,
                        progress: null,
                        tasks: [item.task]
                    }));
                } else if (subCategory) {
                    projectsToRender = externalProjectsData[organizer][subCategory] || [];
                } else {
                    projectsToRender = externalProjectsData[organizer] || [];
                }

                if (projectsToRender.length === 0) {
                    container.innerHTML = `<p class="text-gray-500 text-center">目前無相關活動。</p>`;
                    return;
                }
                
                projectsToRender.forEach(project => {
                    const cardHtml = `
                        <div class="p-6 bg-white rounded-xl shadow-sm">
                            <h3 class="font-bold text-lg mb-2">${project.name}</h3>
                            ${project.team ? `<p class="text-sm text-gray-500 mb-2">參賽團隊：${project.team}</p>` : ''}
                            ${project.progress !== null ? `
                                <div class="mb-4">
                                    <p class="font-medium text-gray-700 mb-1">進度：</p>
                                    <div class="progress-bar">
                                        <div class="progress-fill ${getProgressBarColor(project.progress)}" style="width: ${project.progress}%;"></div>
                                    </div>
                                </div>
                            ` : ''}
                            <ul class="task-list">
                                ${project.tasks.map(task => `
                                    <li>
                                        <div class="flex items-center justify-between">
                                            <span>${task.description}</span>
                                            <span class="status-badge ${getStatusBadgeClass(task.status)}">${getStatusText(task.status)}</span>
                                        </div>
                                    </li>
                                `).join('')}
                            </ul>
                        </div>
                    `;
                    container.innerHTML += cardHtml;
                });
            };

            const getStatusBadgeClass = (status) => {
                switch (status) {
                    case 'completed': return 'status-completed';
                    case 'inprogress': return 'status-inprogress';
                    case 'upcoming': return 'status-upcoming';
                    case 'promoted': return 'status-promoted';
                    case 'award': return 'status-award';
                    default: return '';
                }
            };

            const getStatusText = (status) => {
                switch (status) {
                    case 'completed': return '已完成';
                    case 'inprogress': return '進行中';
                    case 'upcoming': return '待辦';
                    case 'promoted': return '晉級';
                    case 'award': return '獲獎';
                    default: return '未知';
                }
            };

            const getProgressBarColor = (progress) => {
                if (progress >= 100) return 'bg-green-500';
                if (progress >= 75) return 'bg-blue-500';
                if (progress >= 50) return 'bg-yellow-500';
                return 'bg-red-500';
            };

            const tabButtons = document.querySelectorAll('.tab-button');
            const tabContents = document.querySelectorAll('.tab-content');
            const internalSubTabsContainer = document.getElementById('internal-sub-tabs');
            const externalSubTabsContainer = document.getElementById('external-sub-tabs');
            const externalTitle = document.getElementById('external-title');
            
            let activeExternalSubTab = null;

            const renderTopLevelExternalTabs = () => {
                externalSubTabsContainer.innerHTML = '';
                externalTitle.textContent = '所有競賽';
                
                const upcomingButton = document.createElement('button');
                upcomingButton.classList.add('sub-tab-button');
                upcomingButton.textContent = '待辦事項';
                upcomingButton.dataset.organizer = 'upcoming';
                upcomingButton.addEventListener('click', () => {
                    updateExternalSubTab('upcoming');
                });
                externalSubTabsContainer.appendChild(upcomingButton);

                const organizers = Object.keys(externalProjectsData);
                organizers.forEach(organizer => {
                    const button = document.createElement('button');
                    button.classList.add('sub-tab-button');
                    button.textContent = organizer;
                    button.dataset.organizer = organizer;
                    button.addEventListener('click', () => {
                        if (organizer === '醫策會-國家醫療品質獎(NHQA)') {
                            renderNHQASubTabs();
                        } else {
                            updateExternalSubTab(organizer);
                        }
                    });
                    externalSubTabsContainer.appendChild(button);
                });
                updateExternalSubTab('upcoming');
            };

            const renderNHQASubTabs = () => {
                externalSubTabsContainer.innerHTML = '';
                externalTitle.textContent = '國家醫療品質獎(NHQA)';
                
                const backButton = document.createElement('button');
                backButton.classList.add('sub-tab-button');
                backButton.textContent = '返回';
                backButton.addEventListener('click', () => {
                    renderTopLevelExternalTabs();
                });
                externalSubTabsContainer.appendChild(backButton);
                
                const categories = Object.keys(externalProjectsData['醫策會-國家醫療品質獎(NHQA)']);
                categories.forEach(category => {
                    const button = document.createElement('button');
                    button.classList.add('sub-tab-button');
                    button.textContent = category;
                    button.dataset.category = category;
                    button.addEventListener('click', () => {
                        updateExternalSubTab('醫策會-國家醫療品質獎(NHQA)', category);
                    });
                    externalSubTabsContainer.appendChild(button);
                });

                if (categories.length > 0) {
                    updateExternalSubTab('醫策會-國家醫療品質獎(NHQA)', categories[0]);
                }
            };
            
            const updateExternalSubTab = (organizer, subCategory = null) => {
                if (activeExternalSubTab) {
                    activeExternalSubTab.classList.remove('active');
                }
                let newActiveTab;
                if (organizer === '醫策會-國家醫療品質獎(NHQA)') {
                    newActiveTab = document.querySelector(`[data-category="${subCategory}"]`);
                } else {
                    newActiveTab = document.querySelector(`#external-sub-tabs [data-organizer="${organizer}"]`);
                }

                if (newActiveTab) {
                    newActiveTab.classList.add('active');
                    activeExternalSubTab = newActiveTab;
                }
                renderExternalProjects(organizer, subCategory);
            };

            internalSubTabsContainer.querySelectorAll('.sub-tab-button').forEach(button => {
                button.addEventListener('click', () => {
                    internalSubTabsContainer.querySelectorAll('.sub-tab-button').forEach(btn => btn.classList.remove('active'));
                    button.classList.add('active');
                    renderInternalProjects(button.dataset.category);
                });
            });

            tabButtons.forEach(button => {
                button.addEventListener('click', () => {
                    tabButtons.forEach(btn => btn.classList.remove('active'));
                    button.classList.add('active');
                    tabContents.forEach(content => content.classList.add('hidden'));
                    document.getElementById(`${button.dataset.tab}-tab`).classList.remove('hidden');

                    if (button.dataset.tab === 'external') {
                        renderTopLevelExternalTabs();
                    } else {
                        renderInternalProjects('qccTeam');
                    }
                });
            });

            renderInternalProjects('qccTeam');
        });
    </script>
</body>

