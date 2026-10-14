# Deep_versus_surface_Learning_2026
an html table with reference list to compare deep vs surface learning that can be embedded into resources


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Learning Approaches Dashboard</title>
    
    <!-- Tailwind CSS for styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- React & ReactDOM -->
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    
    <!-- Babel for JSX compilation in browser -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc;
            color: #0f172a;
        }
        
        /* Custom scrollbar for table container */
        .table-container::-webkit-scrollbar {
            height: 8px;
        }
        .table-container::-webkit-scrollbar-track {
            background: #f1f5f9;
            border-radius: 4px;
        }
        .table-container::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        .table-container::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        // Reference Database
        const REFERENCES = {
            1: { short: "Marton & Säljö, 1976", full: "Marton, F., & Säljö, R. (1976). On qualitative differences in learning: I—Outcome and process. British Journal of Educational Psychology, 46(1), 4-11." },
            2: { short: "Entwistle & Ramsden, 1983", full: "Entwistle, N. J., & Ramsden, P. (1983). Understanding Student Learning. Croom Helm." },
            3: { short: "Entwistle, 1981", full: "Entwistle, N. J. (1981). Styles of learning and teaching. Wiley." },
            4: { short: "Biggs, 1987", full: "Biggs, J. B. (1987). Student Approaches to Learning and Studying. Australian Council for Educational Research." },
            5: { short: "Prosser & Trigwell, 1999", full: "Prosser, M., & Trigwell, K. (1999). Understanding learning and teaching: The experience in higher education. Society for Research into Higher Education & Open University Press." },
            6: { short: "Kember, 1996", full: "Kember, D. (1996). The intention to both memorise and understand: Another approach to learning? Higher Education, 31(3), 341-354." },
            7: { short: "Winje & Løndal, 2020", full: "Winje, E., & Løndal, K. (2020). Students’ experiences with deep learning. Journal of Further and Higher Education, 44(8), 1085-1098." },
            8: { short: "Biggs, 1979", full: "Biggs, J. B. (1979). Individual differences in study processes and the quality of learning outcomes. Higher Education, 8(4), 381-394." },
            9: { short: "Ramsden, 1992", full: "Ramsden, P. (1992). Learning to teach in higher education. Routledge." },
            10: { short: "Tuononen et al., 2022", full: "Tuononen, T., Parpala, A., & Lindblom-Ylänne, S. (2022). The role of assessment in students’ approaches to learning. Assessment & Evaluation in Higher Education, 47(5), 780-794." },
            11: { short: "Miller & Parlett, 1974", full: "Miller, C. M. L., & Parlett, M. (1974). Up to the mark: A study of the examination game. Society for Research into Higher Education." },
            12: { short: "Kyndt et al., 2011", full: "Kyndt, E., Dochy, F., Struyven, K., & Cascallar, E. (2011). The direct and indirect effect of motivation for learning on students' approaches to learning. Learning and Individual Differences, 21(5), 596-601." },
            13: { short: "Lizzio et al., 2002", full: "Lizzio, A., Wilson, K., & Simons, R. (2002). University students' perceptions of the learning environment and academic outcomes: implications for theory and practice. Studies in Higher Education, 27(1), 27-52." },
            14: { short: "Diseth, 2007", full: "Diseth, A. (2007). Students' evaluation of teaching, approaches to learning, and academic achievement. Scandinavian Journal of Educational Research, 51(2), 185-204." }
        };

        // Dashboard Data Matrix
        const DASHBOARD_DATA = [
            {
                dimension: "Primary Intention",
                deep: { text: "To understand and extract meaning. Seeks to comprehend the underlying concepts.", refId: 1 },
                surface: { text: "To simply cope with task requirements and reproduce information to pass.", refId: 2 },
                strategic: { text: "To maximize grades, achieve academic success, and outcompete peers.", refId: 3 }
            },
            {
                dimension: "Cognitive Processing",
                deep: { text: "Relates new ideas to prior knowledge and integrates discrete facts into holistic structures.", refId: 4 },
                surface: { text: "Treats course units as unrelated bits of knowledge to be memorized unreflectively.", refId: 5 },
                strategic: { text: "Combines memorization with understanding dynamically, shifting depth based on assessment demands.", refId: 6 }
            },
            {
                dimension: "Motivation Source",
                deep: { text: "Driven by intrinsic interest, curiosity, and personal relevance of the subject matter.", refId: 7 },
                surface: { text: "Driven by extrinsic pressure, fear of failure, or task avoidance.", refId: 8 },
                strategic: { text: "Driven by competition, ego-enhancement, and a desire for external accolades.", refId: 2 }
            },
            {
                dimension: "Response to Assessment",
                deep: { text: "Focuses on demonstrating a holistic, integrated understanding and application of knowledge.", refId: 9 },
                surface: { text: "Attempts to predict specific questions and memorize expected answers.", refId: 10 },
                strategic: { text: "Rigorously analyzes marking rubrics, past papers, and specific grader preferences.", refId: 11 }
            },
            {
                dimension: "Reaction to High Workload",
                deep: { text: "Experiences frustration from inadequate time to explore concepts as deeply as desired.", refId: 12 },
                surface: { text: "Defaults heavily to surface coping strategies merely to survive the academic term.", refId: 13 },
                strategic: { text: "Employs ruthless time management, prioritizing high-yield tasks and neglecting others.", refId: 14 }
            }
        ];

        const Citation = ({ refId }) => {
            const refData = REFERENCES[refId];
            if (!refData) return null;

            return (
                <div className="relative group inline-block ml-1 align-super">
                    <a href={`#ref-${refId}`} 
                       className="text-[10px] md:text-xs font-semibold text-indigo-600 bg-indigo-50 hover:bg-indigo-100 hover:text-indigo-800 border border-indigo-200 rounded px-1 py-0.5 transition-colors cursor-pointer"
                       aria-label={`Citation: ${refData.short}`}>
                        [{refId}]
                    </a>
                    
                    {/* Tooltip */}
                    <div className="absolute bottom-full left-1/2 transform -translate-x-1/2 mb-2 hidden group-hover:block w-48 md:w-64 bg-slate-800 text-white text-xs rounded-lg p-3 shadow-xl z-50 transition-opacity opacity-0 group-hover:opacity-100 pointer-events-none">
                        <p className="font-semibold text-indigo-300 mb-1">{refData.short}</p>
                        <p className="text-slate-300 text-[10px] leading-tight line-clamp-3">{refData.full}</p>
                        {/* Caret */}
                        <div className="absolute top-full left-1/2 transform -translate-x-1/2 border-4 border-transparent border-t-slate-800"></div>
                    </div>
                </div>
            );
        };

        const App = () => {
            const [columns, setColumns] = React.useState({
                deep: true,
                surface: true,
                strategic: true
            });

            const toggleColumn = (col) => {
                setColumns(prev => ({
                    ...prev,
                    [col]: !prev[col]
                }));
            };

            return (
                <div className="min-h-screen pb-20">
                    {/* Header */}
                    <header className="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
                        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
                            <h1 className="text-2xl md:text-3xl font-bold text-slate-900 tracking-tight">
                                Academic Learning Approaches Dashboard
                            </h1>
                            <p className="mt-2 text-sm md:text-base text-slate-500 max-w-3xl">
                                An evidence-based comparison of how students conceptualize and approach their studies. 
                                Hover over the citation brackets <span className="inline-block mx-1"><Citation refId={1} /></span> for specific sources.
                            </p>
                            
                            {/* Controls */}
                            <div className="mt-6 flex flex-wrap gap-3 items-center">
                                <span className="text-sm font-medium text-slate-700 mr-2">Toggle Views:</span>
                                
                                <button 
                                    onClick={() => toggleColumn('deep')}
                                    className={`px-4 py-2 rounded-full text-sm font-medium transition-all duration-200 flex items-center gap-2 ${columns.deep ? 'bg-emerald-100 text-emerald-800 border-2 border-emerald-500' : 'bg-slate-100 text-slate-500 border-2 border-transparent hover:bg-slate-200'}`}
                                >
                                    <div className={`w-2 h-2 rounded-full ${columns.deep ? 'bg-emerald-500' : 'bg-slate-400'}`}></div>
                                    Deep Learning
                                </button>
                                
                                <button 
                                    onClick={() => toggleColumn('surface')}
                                    className={`px-4 py-2 rounded-full text-sm font-medium transition-all duration-200 flex items-center gap-2 ${columns.surface ? 'bg-rose-100 text-rose-800 border-2 border-rose-500' : 'bg-slate-100 text-slate-500 border-2 border-transparent hover:bg-slate-200'}`}
                                >
                                    <div className={`w-2 h-2 rounded-full ${columns.surface ? 'bg-rose-500' : 'bg-slate-400'}`}></div>
                                    Surface Learning
                                </button>
                                
                                <button 
                                    onClick={() => toggleColumn('strategic')}
                                    className={`px-4 py-2 rounded-full text-sm font-medium transition-all duration-200 flex items-center gap-2 ${columns.strategic ? 'bg-amber-100 text-amber-800 border-2 border-amber-500' : 'bg-slate-100 text-slate-500 border-2 border-transparent hover:bg-slate-200'}`}
                                >
                                    <div className={`w-2 h-2 rounded-full ${columns.strategic ? 'bg-amber-500' : 'bg-slate-400'}`}></div>
                                    Strategic Learning
                                </button>
                            </div>
                        </div>
                    </header>

                    <main className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
                        {/* Table Container */}
                        <div className="bg-white rounded-xl shadow-md border border-slate-200 overflow-hidden">
                            <div className="overflow-x-auto table-container">
                                <table className="w-full text-left border-collapse">
                                    <thead>
                                        <tr>
                                            <th className="bg-slate-50 p-4 border-b border-slate-200 font-semibold text-slate-700 w-1/5 min-w-[150px] sticky left-0 z-20 shadow-[2px_0_5px_rgba(0,0,0,0.02)]">
                                                Cognitive Dimension
                                            </th>
                                            {columns.deep && (
                                                <th className="bg-emerald-50 p-4 border-b border-l border-emerald-200 font-bold text-emerald-800 w-1/4 min-w-[250px]">
                                                    Deep Approach
                                                </th>
                                            )}
                                            {columns.surface && (
                                                <th className="bg-rose-50 p-4 border-b border-l border-rose-200 font-bold text-rose-800 w-1/4 min-w-[250px]">
                                                    Surface Approach
                                                </th>
                                            )}
                                            {columns.strategic && (
                                                <th className="bg-amber-50 p-4 border-b border-l border-amber-200 font-bold text-amber-800 w-1/4 min-w-[250px]">
                                                    Strategic Approach
                                                </th>
                                            )}
                                        </tr>
                                    </thead>
                                    <tbody className="divide-y divide-slate-200">
                                        {DASHBOARD_DATA.map((row, idx) => (
                                            <tr key={idx} className="hover:bg-slate-50/50 transition-colors">
                                                <td className="p-4 align-top font-medium text-slate-800 bg-white sticky left-0 z-10 shadow-[2px_0_5px_rgba(0,0,0,0.02)]">
                                                    {row.dimension}
                                                </td>
                                                
                                                {columns.deep && (
                                                    <td className="p-4 align-top border-l border-slate-200 text-slate-600 leading-relaxed">
                                                        {row.deep.text}
                                                        <Citation refId={row.deep.refId} />
                                                    </td>
                                                )}
                                                
                                                {columns.surface && (
                                                    <td className="p-4 align-top border-l border-slate-200 text-slate-600 leading-relaxed">
                                                        {row.surface.text}
                                                        <Citation refId={row.surface.refId} />
                                                    </td>
                                                )}
                                                
                                                {columns.strategic && (
                                                    <td className="p-4 align-top border-l border-slate-200 text-slate-600 leading-relaxed">
                                                        {row.strategic.text}
                                                        <Citation refId={row.strategic.refId} />
                                                    </td>
                                                )}
                                            </tr>
                                        ))}
                                    </tbody>
                                </table>
                            </div>
                        </div>

                        {/* References Section */}
                        <div className="mt-16 bg-slate-50 rounded-xl p-6 md:p-8 border border-slate-200">
                            <h2 className="text-xl font-bold text-slate-800 mb-6 flex items-center">
                                <svg className="w-5 h-5 mr-2 text-indigo-500" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253" /></svg>
                                Evidence Base & References
                            </h2>
                            <ul className="space-y-4 text-sm text-slate-600">
                                {Object.entries(REFERENCES).map(([id, data]) => (
                                    <li key={id} id={`ref-${id}`} className="flex gap-4 target:bg-indigo-100 target:p-2 target:rounded-md transition-all duration-300">
                                        <span className="font-semibold text-indigo-600 min-w-[24px]">[{id}]</span>
                                        <span className="leading-relaxed">{data.full}</span>
                                    </li>
                                ))}
                            </ul>
                        </div>
                    </main>
                </div>
            );
        };

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
