<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PRISM 성격 진단 테스트</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        
        .container {
            max-width: 900px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .header {
            background: white;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            text-align: center;
            margin-bottom: 30px;
        }
        
        .header h1 {
            color: #4a5568;
            font-size: 2.5em;
            margin-bottom: 10px;
            font-weight: 700;
        }
        
        .header .subtitle {
            color: #718096;
            font-size: 1.2em;
            margin-bottom: 20px;
        }
        
        .info-box {
            background: #f7fafc;
            padding: 20px;
            border-radius: 10px;
            border-left: 5px solid #4299e1;
            margin-bottom: 20px;
        }
        
        .test-container {
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        
        .progress-container {
            margin-bottom: 30px;
        }
        
        .progress-info {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
            font-weight: 600;
            color: #4a5568;
        }
        
        .progress-bar {
            width: 100%;
            height: 12px;
            background: #e2e8f0;
            border-radius: 6px;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            width: 0%;
            transition: width 0.3s ease;
        }
        
        .question-container {
            background: #f8f9fa;
            padding: 30px;
            border-radius: 15px;
            border-left: 5px solid #667eea;
            margin-bottom: 30px;
        }
        
        .dimension-title {
            font-size: 1.1em;
            font-weight: 600;
            color: #667eea;
            margin-bottom: 5px;
        }
        
        .question-number {
            font-size: 1.4em;
            font-weight: 700;
            color: #2d3748;
            margin-bottom: 15px;
        }
        
        .question-text {
            font-size: 1.2em;
            font-weight: 500;
            color: #2d3748;
            margin-bottom: 25px;
            line-height: 1.5;
        }
        
        .options {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }
        
        .option {
            padding: 20px;
            background: white;
            border: 2px solid #e2e8f0;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1.1em;
            position: relative;
        }
        
        .option:hover {
            border-color: #667eea;
            background: #f7fafc;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .option.selected {
            border-color: #667eea;
            background: #667eea;
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102,126,234,0.3);
        }
        
        .option-number {
            font-weight: 700;
            color: #667eea;
            margin-right: 10px;
        }
        
        .option.selected .option-number {
            color: white;
        }
        
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 30px;
        }
        
        .nav-btn {
            padding: 15px 30px;
            border: none;
            border-radius: 50px;
            font-size: 1.1em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .prev-btn {
            background: #e2e8f0;
            color: #4a5568;
        }
        
        .prev-btn:hover {
            background: #cbd5e0;
            transform: translateY(-2px);
        }
        
        .next-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }
        
        .next-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }
        
        .next-btn:disabled {
            background: #e2e8f0;
            color: #a0aec0;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .results {
            display: none;
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
        }
        
        .result-header {
            text-align: center;
            margin-bottom: 40px;
        }
        
        .result-type {
            font-size: 3em;
            font-weight: 700;
            color: #667eea;
            margin-bottom: 10px;
            letter-spacing: 3px;
        }
        
        .result-title {
            font-size: 1.8em;
            color: #2d3748;
            margin-bottom: 20px;
        }
        
        .dimensions-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 40px;
        }
        
        .dimension-result {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 12px;
            border-left: 4px solid #667eea;
        }
        
        .dimension-name {
            font-weight: 600;
            color: #2d3748;
            margin-bottom: 8px;
            font-size: 1.1em;
        }
        
        .dimension-value {
            font-size: 2em;
            font-weight: 700;
            color: #667eea;
            margin-bottom: 5px;
        }
        
        .dimension-desc {
            color: #4a5568;
            line-height: 1.4;
        }
        
        .result-section {
            margin: 30px 0;
            padding: 25px;
            background: #f0f8ff;
            border-radius: 15px;
            border-left: 5px solid #4299e1;
        }
        
        .section-title {
            font-size: 1.4em;
            font-weight: 600;
            color: #2c5aa0;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
        }
        
        .section-icon {
            margin-right: 10px;
            font-size: 1.2em;
        }
        
        .compatibility-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }
        
        .compatibility-item {
            background: white;
            padding: 15px;
            border-radius: 10px;
            border-left: 4px solid #48bb78;
        }
        
        .compatibility-type {
            font-weight: 600;
            color: #2d3748;
            margin-bottom: 5px;
        }
        
        .compatibility-desc {
            color: #4a5568;
            font-size: 0.9em;
        }
        
        .job-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }
        
        .job-item {
            background: white;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            border: 2px solid #e2e8f0;
            transition: all 0.3s ease;
        }
        
        .job-item:hover {
            border-color: #667eea;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .job-title {
            font-weight: 600;
            color: #2d3748;
            margin-bottom: 5px;
        }
        
        .job-match {
            color: #48bb78;
            font-weight: 600;
            font-size: 0.9em;
        }
        
        .restart-btn {
            background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 50px;
            font-size: 1.1em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            margin: 30px auto;
            display: block;
        }
        
        .restart-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .test-container, .results {
                padding: 20px;
            }
            
            .header h1 {
                font-size: 2em;
            }
            
            .options {
                gap: 10px;
            }
            
            .option {
                padding: 15px;
                font-size: 1em;
            }
            
            .result-type {
                font-size: 2.2em;
                letter-spacing: 2px;
            }
            
            .dimensions-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>PRISM 성격 진단</h1>
            <p class="subtitle">7차원 × 4단계 = 16,384가지 정밀 성격 분석</p>
            <div class="info-box">
                <strong>📊 가장 정확한 성격 테스트</strong><br>
                총 42문항 | 소요시간: 약 15-20분<br>
                구체적 상황 기반으로 정확한 성격 분석
            </div>
        </div>
        
        <div class="test-container" id="testContainer">
            <div class="progress-container">
                <div class="progress-info">
                    <span>진행률</span>
                    <span id="progressText">1 / 42</span>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" id="progressFill"></div>
                </div>
            </div>
            
            <div class="question-container">
                <div class="dimension-title" id="dimensionTitle">에너지 방향성 (Energy Direction)</div>
                <div class="question-number" id="questionNumber">Q1.</div>
                <div class="question-text" id="questionText"></div>
                
                <div class="options" id="optionsContainer">
                    <div class="option" data-value="1">
                        <span class="option-number">1)</span>
                        <span class="option-text"></span>
                    </div>
                    <div class="option" data-value="2">
                        <span class="option-number">2)</span>
                        <span class="option-text"></span>
                    </div>
                    <div class="option" data-value="3">
                        <span class="option-number">3)</span>
                        <span class="option-text"></span>
                    </div>
                    <div class="option" data-value="4">
                        <span class="option-number">4)</span>
                        <span class="option-text"></span>
                    </div>
                </div>
            </div>
            
            <div class="navigation">
                <button class="nav-btn prev-btn" id="prevBtn" onclick="prevQuestion()">이전</button>
                <button class="nav-btn next-btn" id="nextBtn" onclick="nextQuestion()" disabled>다음</button>
            </div>
        </div>
        
        <div class="results" id="results">
            <div class="result-header">
                <div class="result-type" id="resultType">CHJPS33</div>
                <div class="result-title" id="resultTitle">창의적 협력가형</div>
            </div>
            
            <div class="dimensions-grid" id="dimensionsGrid">
                <!-- 차원별 결과가 여기에 동적으로 생성됩니다 -->
            </div>
            
            <div class="result-section">
                <div class="section-title">
                    <span class="section-icon">💕</span>
                    호환되는 성격 유형
                </div>
                <div class="compatibility-grid" id="compatibilityGrid">
                    <!-- 호환성 결과가 여기에 동적으로 생성됩니다 -->
                </div>
            </div>
            
            <div class="result-section">
                <div class="section-title">
                    <span class="section-icon">💼</span>
                    추천 직업
                </div>
                <div class="job-grid" id="jobGrid">
                    <!-- 직업 추천이 여기에 동적으로 생성됩니다 -->
                </div>
            </div>
            
            <button class="restart-btn" onclick="restartTest()">다시 테스트하기</button>
        </div>
    </div>
    
    <script>
        // 테스트 데이터
        const questions = [
            // 에너지 방향성 (1-6)
            {
                dimension: "에너지 방향성 (Energy Direction)",
                text: "금요일 오후 6시, 한 주간의 일이 끝났습니다. 첫 번째로 하고 싶은 일은?",
                options: [
                    "동료들에게 \"오늘 회식하자!\"라고 제안한다",
                    "친한 동료 2-3명과 가벼운 저녁 식사를 한다",
                    "혼자 있을지 누군가와 만날지 그때 기분에 따라 결정한다",
                    "집에 가서 혼자만의 시간을 갖는다"
                ]
            },
            {
                dimension: "에너지 방향성 (Energy Direction)",
                text: "새로운 프로젝트에 대한 아이디어가 떠올랐습니다. 가장 먼저 하는 행동은?",
                options: [
                    "즉시 동료들을 불러서 브레인스토밍을 시작한다",
                    "아이디어를 정리한 후 신뢰하는 동료에게 먼저 얘기한다",
                    "혼자 충분히 생각해본 후 필요하면 다른 사람과 논의한다",
                    "혼자서 완전히 구체화시킨 후 발표한다"
                ]
            },
            {
                dimension: "에너지 방향성 (Energy Direction)",
                text: "회사 워크숍에서 \"자유롭게 네트워킹하는 시간\"이 주어졌습니다. 당신은?",
                options: [
                    "적극적으로 여러 사람에게 다가가서 대화를 시작한다",
                    "아는 사람들과 대화하다가 자연스럽게 새로운 사람들과도 만난다",
                    "누군가 다가오면 대화하지만 먼저 다가가지는 않는다",
                    "조용한 곳에서 한두 명과만 깊은 대화를 나눈다"
                ]
            },
            {
                dimension: "에너지 방향성 (Energy Direction)",
                text: "점심시간에 혼자 있게 되었습니다. 어떻게 보내시겠습니까?",
                options: [
                    "다른 팀 사람들에게 가서 함께 먹자고 제안한다",
                    "동료에게 연락해서 함께 먹을 사람을 찾는다",
                    "상황에 따라 혼자 먹거나 누군가와 함께 먹는다",
                    "혼자 조용한 곳에서 먹으며 개인 시간을 즐긴다"
                ]
            },
            {
                dimension: "에너지 방향성 (Energy Direction)",
                text: "주말에 친구가 \"큰 파티에 같이 가자\"고 제안했습니다. 솔직한 반응은?",
                options: [
                    "\"좋아! 언제 어디서? 다른 친구들도 불러보자!\"",
                    "\"좋아, 가보자. 어떤 사람들이 올 예정이야?\"",
                    "\"음.. 어떤 파티인지 자세히 알려줘. 생각해볼게\"",
                    "\"파티보다는 우리끼리 조용히 만나는 게 어때?\""
                ]
            },
            {
                dimension: "에너지 방향성 (Energy Direction)",
                text: "새로운 부서로 이동 첫날, 부서원들과 처음 만났습니다. 당신의 행동은?",
                options: [
                    "적극적으로 자기소개하고 모든 사람에게 먼저 말을 건다",
                    "자기소개는 하되 상대방이 대화를 이어가길 기다린다",
                    "상황을 지켜보다가 적절한 타이밍에 대화에 참여한다",
                    "업무에 필요한 최소한의 대화만 하고 적응 시간을 갖는다"
                ]
            },
            // 정보 처리 방식 (7-12)
            {
                dimension: "정보 처리 방식 (Information Processing)",
                text: "새로운 업무 프로그램을 배워야 합니다. 가장 선호하는 학습 방법은?",
                options: [
                    "매뉴얼을 처음부터 끝까지 차근차근 읽으며 단계별로 따라한다",
                    "기본 기능은 매뉴얼로, 심화 기능은 직접 실습하며 배운다",
                    "전체적인 구조를 파악한 후 필요한 부분을 집중적으로 배운다",
                    "일단 전체를 훑어보고 직관적으로 사용법을 터득한다"
                ]
            },
            {
                dimension: "정보 처리 방식 (Information Processing)",
                text: "복잡한 문제가 발생했습니다. 해결 과정은?",
                options: [
                    "문제를 세분화해서 하나씩 차례대로 해결한다",
                    "중요한 부분과 세부 사항을 구분해서 우선순위대로 처리한다",
                    "전체 상황을 파악하고 핵심 원인을 찾아 해결한다",
                    "직감적으로 해결 방향을 정하고 창의적인 방법을 시도한다"
                ]
            },
            {
                dimension: "정보 처리 방식 (Information Processing)",
                text: "새로운 도시로 여행을 계획하고 있습니다. 정보 수집 방법은?",
                options: [
                    "가이드북을 사서 명소, 교통, 숙박을 체계적으로 조사한다",
                    "주요 관광지와 맛집 정보를 위주로 실용적으로 조사한다",
                    "여행 테마를 정하고 관련된 장소들을 연결해서 계획한다",
                    "대략적인 정보만 보고 현지에서 즉흥적으로 발견하고 싶다"
                ]
            },
            {
                dimension: "정보 처리 방식 (Information Processing)",
                text: "회의에서 새로운 마케팅 전략을 제안해야 합니다. 접근 방법은?",
                options: [
                    "경쟁사 분석, 시장 데이터, 과거 사례를 꼼꼼히 조사해서 제안한다",
                    "핵심 데이터와 실무진 의견을 종합해서 실현 가능한 방안을 제시한다",
                    "시장 트렌드와 고객 니즈를 분석해서 전략적 방향을 제안한다",
                    "혁신적인 아이디어와 창의적 접근법을 중심으로 제안한다"
                ]
            },
            {
                dimension: "정보 처리 방식 (Information Processing)",
                text: "책을 읽을 때 선호하는 방식은?",
                options: [
                    "첫 페이지부터 순서대로, 중요한 부분은 따로 정리하며 읽는다",
                    "목차를 보고 필요한 부분을 우선적으로, 나머지는 시간 날 때 읽는다",
                    "전체 구조를 파악한 후 관심 있는 부분을 깊이 있게 읽는다",
                    "아무 페이지나 펼쳐서 흥미로운 부분부터 자유롭게 읽는다"
                ]
            },
            {
                dimension: "정보 처리 방식 (Information Processing)",
                text: "새로운 요리를 만들어보려고 합니다. 어떻게 시작하시겠습니까?",
                options: [
                    "정확한 레시피를 찾아서 재료와 순서를 정확히 따른다",
                    "기본 레시피를 참고하되 취향에 맞게 조금씩 변형한다",
                    "요리의 원리를 이해하고 비슷한 요리 경험을 활용한다",
                    "대략적인 방법만 알고 직감과 센스로 만들어본다"
                ]
            },
            // 의사 결정 방식 (13-18)
            {
                dimension: "의사 결정 방식 (Decision Making)",
                text: "팀 프로젝트에서 의견이 나뉘었습니다. 최종 결정을 내리는 기준은?",
                options: [
                    "객관적 데이터와 논리적 근거가 가장 확실한 방안",
                    "논리적 타당성과 팀 의견을 종합적으로 고려한 방안",
                    "팀원들의 감정과 의견을 고려하되 합리성도 있는 방안",
                    "모든 팀원이 편하고 만족할 수 있는 방안"
                ]
            },
            {
                dimension: "의사 결정 방식 (Decision Making)",
                text: "친구가 잘못된 결정을 하려고 합니다. 어떻게 조언하시겠습니까?",
                options: [
                    "객관적 사실과 논리로 왜 잘못되었는지 명확히 설명한다",
                    "근거를 제시하되 친구의 기분도 상하지 않게 말한다",
                    "친구의 마음을 먼저 이해하고 조심스럽게 다른 관점을 제시한다",
                    "친구의 기분을 상하지 않게 돌려서 말하거나 조용히 지켜본다"
                ]
            },
            {
                dimension: "의사 결정 방식 (Decision Making)",
                text: "부서 내 갈등 상황을 해결해야 합니다. 접근 방법은?",
                options: [
                    "사실관계를 명확히 파악하고 규정에 따라 공정하게 처리한다",
                    "객관적 판단과 관련자들의 입장을 모두 고려해서 해결한다",
                    "갈등 당사자들의 감정을 충분히 들어본 후 조화로운 해결책을 찾는다",
                    "모든 사람이 상처받지 않고 관계가 회복될 수 있는 방법을 찾는다"
                ]
            },
            {
                dimension: "의사 결정 방식 (Decision Making)",
                text: "새로운 프로젝트의 우선순위를 정해야 합니다. 판단 기준은?",
                options: [
                    "비용 대비 효과, ROI, 리스크 분석을 기반으로 결정한다",
                    "수치적 분석과 팀의 역량, 상황을 종합적으로 고려한다",
                    "팀원들의 관심사와 회사 분위기, 장기적 만족도를 고려한다",
                    "모든 구성원이 의미를 느끼고 즐겁게 참여할 수 있는 프로젝트를 선택한다"
                ]
            },
            {
                dimension: "의사 결정 방식 (Decision Making)",
                text: "고객 불만이 접수되었습니다. 처리 방식은?",
                options: [
                    "사실관계 확인 후 규정에 따라 명확하고 일관성 있게 처리한다",
                    "규정을 기본으로 하되 고객 상황도 어느 정도 고려해서 처리한다",
                    "고객의 감정과 상황을 충분히 이해한 후 최대한 만족할 만한 해결책을 찾는다",
                    "고객이 기분 상하지 않고 좋은 인상을 갖도록 최대한 배려해서 처리한다"
                ]
            },
            {
                dimension: "의사 결정 방식 (Decision Making)",
                text: "성과 평가를 해야 하는 상황입니다. 평가 기준은?",
                options: [
                    "객관적 지표와 성과 데이터만을 기준으로 공정하게 평가한다",
                    "정량적 성과와 업무 태도, 개선 노력을 균형있게 평가한다",
                    "개인의 상황과 노력 과정, 팀에 미친 긍정적 영향을 중요하게 본다",
                    "개인의 성장과 팀 화합에 기여한 정도를 가장 중요하게 평가한다"
                ]
            },
            // 생활 패턴 (19-24)
            {
                dimension: "생활 패턴 (Lifestyle Pattern)",
                text: "중요한 출장이 1주일 후에 있습니다. 준비 방식은?",
                options: [
                    "출장 1주일 전부터 체크리스트를 만들어 매일 조금씩 준비한다",
                    "2-3일 전부터 계획적으로 필요한 것들을 차례로 준비한다",
                    "전날까지 대략 준비하고 당일 아침에 마무리한다",
                    "당일 아침이나 출발 직전에 급하게 필요한 것만 챙긴다"
                ]
            },
            {
                dimension: "생활 패턴 (Lifestyle Pattern)",
                text: "1년 휴가 계획을 세운다면?",
                options: [
                    "6개월 전부터 항공편, 숙박, 상세 일정을 모두 예약하고 준비한다",
                    "한 달 전에 큰 틀을 정하고 2주 전에 세부사항을 준비한다",
                    "1주일 전에 숙박과 교통편만 예약하고 나머지는 현지에서 결정한다",
                    "떠나고 싶을 때 즉흥적으로 떠나거나 최소한만 예약한다"
                ]
            },
            {
                dimension: "생활 패턴 (Lifestyle Pattern)",
                text: "새로운 프로젝트가 배정되었습니다. 일정 관리 방식은?",
                options: [
                    "전체 기간을 세분화해서 매일매일 해야 할 일을 구체적으로 계획한다",
                    "주요 마일스톤을 설정하고 주간 단위로 계획을 세운다",
                    "마감일만 정하고 진행하면서 상황에 따라 유연하게 조정한다",
                    "특별한 계획 없이 영감이 올 때마다 집중적으로 작업한다"
                ]
            },
            {
                dimension: "생활 패턴 (Lifestyle Pattern)",
                text: "방 정리/청소는 언제 하시나요?",
                options: [
                    "매일 정해진 시간에 조금씩, 일주일에 한 번은 대청소한다",
                    "주말마다 정기적으로, 필요할 때마다 부분적으로 한다",
                    "너무 지저분해지면 하거나 시간 날 때 몰아서 한다",
                    "정말 필요할 때만 하거나 누군가 올 때만 급하게 한다"
                ]
            },
            {
                dimension: "생활 패턴 (Lifestyle Pattern)",
                text: "쇼핑할 때의 방식은?",
                options: [
                    "미리 목록을 만들고 예산을 정해서 계획적으로 쇼핑한다",
                    "대략적인 목록은 있지만 현장에서 필요한 것을 추가로 구매한다",
                    "필요한 것만 생각하고 가서 보이는 대로 구매한다",
                    "특별한 계획 없이 가서 마음에 드는 것을 즉흥적으로 구매한다"
                ]
            },
            {
                dimension: "생활 패턴 (Lifestyle Pattern)",
                text: "일주일 식단은 어떻게 관리하시나요?",
                options: [
                    "일주일 식단을 미리 짜고 주말에 식재료를 한 번에 구매한다",
                    "2-3일치 정도 계획하고 그때그때 부족한 것을 보충한다",
                    "특별한 계획 없이 그날그날 냉장고에 있는 것으로 해결한다",
                    "먹고 싶은 것이 있을 때 그때마다 사러 가거나 주문한다"
                ]
            },
            // 스트레스 반응성 (25-30)
            {
                dimension: "스트레스 반응성 (Stress Response)",
                text: "중요한 발표를 하루 앞두고 있습니다. 현재 상태는?",
                options: [
                    "평소와 다름없이 차분하고 안정적이다",
                    "약간 긴장되지만 곧 평정심을 되찾는다",
                    "상당히 긴장되지만 어떻게든 잘 해낼 것이다",
                    "매우 불안하고 긴장되어 잠을 잘 못 잔다"
                ]
            },
            {
                dimension: "스트레스 반응성 (Stress Response)",
                text: "갑작스럽게 여러 문제가 동시에 발생했습니다. 반응은?",
                options: [
                    "차분하게 우선순위를 정해서 하나씩 해결한다",
                    "잠깐 당황하지만 빠르게 마음을 가다듬고 대응책을 마련한다",
                    "스트레스를 받지만 시간을 두고 차근차근 해결한다",
                    "매우 힘들어하고 감정적으로 불안정해진다"
                ]
            },
            {
                dimension: "스트레스 반응성 (Stress Response)",
                text: "상사에게 예상치 못한 비판을 받았습니다. 당신의 반응은?",
                options: [
                    "객관적으로 받아들이고 개선점을 찾아 행동한다",
                    "처음엔 기분 나쁘지만 곧 건설적으로 받아들인다",
                    "기분이 상하고 스트레스를 받지만 시간이 지나면 수용한다",
                    "매우 상처받고 한동안 그 일이 계속 마음에 걸린다"
                ]
            },
            {
                dimension: "스트레스 반응성 (Stress Response)",
                text: "실수로 중요한 업무를 놓쳤을 때 반응은?",
                options: [
                    "즉시 해결 방안을 찾고 재발 방지책을 마련한다",
                    "잠깐 당황하지만 빠르게 수습하고 사과한다",
                    "자책하면서도 최대한 빨리 만회하려고 노력한다",
                    "매우 자책하고 한동안 그 일로 우울해한다"
                ]
            },
            {
                dimension: "스트레스 반응성 (Stress Response)",
                text: "새로운 환경에 적응해야 하는 상황입니다. 어떻게 느끼시나요?",
                options: [
                    "새로운 도전으로 받아들이고 차분하게 적응한다",
                    "처음엔 낯설지만 곧 흥미롭게 받아들인다",
                    "약간 불안하지만 시간이 지나면 적응할 것이다",
                    "매우 불안하고 스트레스를 많이 받는다"
                ]
            },
            {
                dimension: "스트레스 반응성 (Stress Response)",
                text: "갈등 상황에 처했을 때 신체적/정서적 반응은?",
                options: [
                    "거의 변화가 없고 평상시와 똑같다",
                    "약간 긴장되지만 곧 평정심을 되찾는다",
                    "심장이 뛰고 긴장되지만 견딜 만하다",
                    "심장이 빨리 뛰고 손이 떨리며 매우 불편하다"
                ]
            },
            // 변화 적응성 (31-36)
            {
                dimension: "변화 적응성 (Change Adaptability)",
                text: "회사에서 업무 시스템을 완전히 바꾼다고 발표했습니다. 첫 반응은?",
                options: [
                    "\"기존 방식이 더 효율적인데 왜 바꾸는 거지?\" 하며 반대 의견을 낸다",
                    "\"충분한 교육과 준비 기간을 거쳐서 단계적으로 도입하자\"고 제안한다",
                    "\"변화가 필요하다면 빨리 배워서 적응해보자\"고 생각한다",
                    "\"드디어! 새로운 시스템으로 더 혁신적으로 일할 수 있겠다\"며 기대한다"
                ]
            },
            {
                dimension: "변화 적응성 (Change Adaptability)",
                text: "평소 가던 맛집이 문을 닫았습니다. 어떻게 하시겠습니까?",
                options: [
                    "비슷한 메뉴를 파는 다른 익숙한 식당을 찾는다",
                    "지인에게 추천을 받아서 검증된 곳으로 간다",
                    "이번 기회에 새로운 종류의 음식을 시도해본다",
                    "완전히 다른 새로운 곳을 탐험하는 재미를 즐긴다"
                ]
            },
            {
                dimension: "변화 적응성 (Change Adaptability)",
                text: "새로운 기술/트렌드가 나타났을 때 태도는?",
                options: [
                    "\"기존 방식도 충분히 좋은데 굳이 바꿀 필요가 있나?\"",
                    "\"시간을 두고 지켜본 후 정말 좋으면 도입하자\"",
                    "\"유용해 보이니까 배워서 활용해보자\"",
                    "\"재밌겠다! 가장 먼저 시도해보고 다른 사람들에게도 알려주자\""
                ]
            },
            {
                dimension: "변화 적응성 (Change Adaptability)",
                text: "여행 계획이 예상과 다르게 흘러갈 때 반응은?",
                options: [
                    "원래 계획대로 하려고 최대한 노력한다",
                    "계획을 수정해서 비슷한 대안을 찾는다",
                    "계획 변경을 받아들이고 새로운 경험을 즐긴다",
                    "\"더 재미있는 모험이 될 것 같다!\"며 즐겁게 받아들인다"
                ]
            },
            {
                dimension: "변화 적응성 (Change Adaptability)",
                text: "새로운 업무 방식을 제안받았을 때 반응은?",
                options: [
                    "\"지금까지 이 방식으로 잘 해왔는데 왜 바꿔야 하나요?\"",
                    "\"장단점을 충분히 검토해본 후에 결정하면 좋겠어요\"",
                    "\"괜찮은 아이디어네요. 한번 시도해볼까요?\"",
                    "\"혁신적이네요! 당장 시작해봅시다!\""
                ]
            },
            {
                dimension: "변화 적응성 (Change Adaptability)",
                text: "갑작스러운 계획 변경 상황에서 기분은?",
                options: [
                    "짜증나고 불편하다",
                    "처음엔 당황스럽지만 어쩔 수 없다고 받아들인다",
                    "약간 아쉽지만 새로운 계획도 나쁘지 않다",
                    "오히려 더 흥미롭고 기대된다"
                ]
            },
            // 사회적 상호작용 (37-42)
            {
                dimension: "사회적 상호작용 (Social Interaction)",
                text: "팀 프로젝트에서 의견 충돌이 생겼습니다. 대응 방식은?",
                options: [
                    "내 의견이 옳다는 근거를 명확히 제시하며 설득한다",
                    "상대방 의견도 듣되 더 나은 방안을 논리적으로 제시한다",
                    "상대방 입장을 충분히 이해한 후 조심스럽게 다른 의견을 제시한다",
                    "갈등을 피하고 상대방 의견에 맞춰주거나 타협점을 찾는다"
                ]
            },
            {
                dimension: "사회적 상호작용 (Social Interaction)",
                text: "승진 기회가 생겼는데 동료도 같이 지원한다고 합니다. 어떻게 하시겠습니까?",
                options: [
                    "당연히 내가 더 적합하다는 것을 어필하며 적극적으로 경쟁한다",
                    "공정한 경쟁을 위해 실력으로 승부하되 동료와의 관계도 고려한다",
                    "동료와의 관계를 해치지 않는 선에서 나의 장점을 어필한다",
                    "동료가 더 원한다면 양보하거나 함께 할 수 있는 방법을 찾는다"
                ]
            },
            {
                dimension: "사회적 상호작용 (Social Interaction)",
                text: "팀 내에서 당신의 역할은 주로 무엇인가요?",
                options: [
                    "목표를 설정하고 팀을 이끌어가는 리더 역할",
                    "필요할 때 리더십을 발휘하되 상황에 따라 역할을 조절",
                    "팀원들의 의견을 듣고 조율하는 중재자 역할",
                    "팀 분위기를 좋게 만들고 모든 사람이 편할 수 있도록 배려"
                ]
            },
            {
                dimension: "사회적 상호작용 (Social Interaction)",
                text: "회의에서 다른 의견을 제시해야 할 때 방식은?",
                options: [
                    "\"제 생각에는 이 방법이 더 효과적일 것 같습니다\"라고 직접적으로 말한다",
                    "\"다른 관점에서 보면...\"이라며 논리적 근거와 함께 제시한다",
                    "\"혹시 이런 방법은 어떨까요?\"라며 조심스럽게 제안한다",
                    "\"모두의 의견이 좋은데, 이것도 고려해볼 만할 것 같아요\"라며 부드럽게 제시한다"
                ]
            },
            {
                dimension: "사회적 상호작용 (Social Interaction)",
                text: "동료가 실수했을 때 어떻게 대응하시나요?",
                options: [
                    "실수의 문제점을 명확히 지적하고 개선 방안을 제시한다",
                    "실수를 지적하되 상대방의 기분도 고려해서 건설적으로 말한다",
                    "상대방이 스스로 깨달을 수 있도록 조심스럽게 힌트를 준다",
                    "직접 지적하기보다는 도움을 주거나 조용히 넘어간다"
                ]
            },
            {
                dimension: "사회적 상호작용 (Social Interaction)",
                text: "성과에 대한 인정을 받을 때 반응은?",
                options: [
                    "\"당연한 결과입니다. 더 좋은 성과를 내겠습니다\"",
                    "\"감사합니다. 팀원들과 함께 노력한 결과입니다\"",
                    "\"과찬의 말씀입니다. 팀원들 덕분에 가능했습니다\"",
                    "\"정말 감사합니다. 모든 분들 덕분입니다\""
                ]
            }
        ];
        
        // 차원 정보
        const dimensions = [
            { name: "에너지 방향성", codes: ["A", "B", "C", "D"], descriptions: ["매우 외향적", "약간 외향적", "약간 내향적", "매우 내향적"] },
            { name: "정보 처리", codes: ["E", "F", "G", "H"], descriptions: ["현실적", "약간 현실적", "약간 직관적", "직관적"] },
            { name: "의사 결정", codes: ["I", "J", "K", "L"], descriptions: ["논리적", "약간 논리적", "약간 감정적", "감정적"] },
            { name: "생활 패턴", codes: ["M", "N", "O", "P"], descriptions: ["계획적", "약간 계획적", "약간 즉흥적", "즉흥적"] },
            { name: "스트레스 반응", codes: ["Q", "R", "S", "T"], descriptions: ["매우 안정적", "안정적", "민감함", "매우 민감함"] },
            { name: "변화 적응성", codes: ["1", "2", "3", "4"], descriptions: ["보수적", "신중함", "적응적", "혁신적"] },
            { name: "사회적 상호작용", codes: ["1", "2", "3", "4"], descriptions: ["경쟁적", "적극적", "협력적", "조화형"] }
        ];
        
        // 테스트 상태
        let currentQuestion = 0;
        let answers = new Array(42).fill(null);
        
        // DOM 요소
        const progressFill = document.getElementById('progressFill');
        const progressText = document.getElementById('progressText');
        const dimensionTitle = document.getElementById('dimensionTitle');
        const questionNumber = document.getElementById('questionNumber');
        const questionText = document.getElementById('questionText');
        const options = document.querySelectorAll('.option');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const testContainer = document.getElementById('testContainer');
        const results = document.getElementById('results');
        
        // 초기화
        function initTest() {
            currentQuestion = 0;
            answers = new Array(42).fill(null);
            showQuestion();
            updateProgress();
            updateNavigation();
        }
        
        // 질문 표시
        function showQuestion() {
            const question = questions[currentQuestion];
            
            dimensionTitle.textContent = question.dimension;
            questionNumber.textContent = `Q${currentQuestion + 1}.`;
            questionText.textContent = question.text;
            
            options.forEach((option, index) => {
                const optionText = option.querySelector('.option-text');
                optionText.textContent = question.options[index];
                
                option.classList.remove('selected');
                if (answers[currentQuestion] === index + 1) {
                    option.classList.add('selected');
                }
            });
        }
        
        // 진행률 업데이트
        function updateProgress() {
            const progress = ((currentQuestion + 1) / 42) * 100;
            progressFill.style.width = progress + '%';
            progressText.textContent = `${currentQuestion + 1} / 42`;
        }
        
        // 네비게이션 버튼 상태 업데이트
        function updateNavigation() {
            prevBtn.style.display = currentQuestion === 0 ? 'none' : 'block';
            nextBtn.disabled = answers[currentQuestion] === null;
            
            if (currentQuestion === 41) {
                nextBtn.textContent = '결과 보기';
            } else {
                nextBtn.textContent = '다음';
            }
        }
        
        // 옵션 선택 이벤트
        options.forEach((option, index) => {
            option.addEventListener('click', () => {
                options.forEach(opt => opt.classList.remove('selected'));
                option.classList.add('selected');
                answers[currentQuestion] = index + 1;
                updateNavigation();
            });
        });
        
        // 이전 질문
        function prevQuestion() {
            if (currentQuestion > 0) {
                currentQuestion--;
                showQuestion();
                updateProgress();
                updateNavigation();
            }
        }
        
        // 다음 질문
        function nextQuestion() {
            if (answers[currentQuestion] !== null) {
                if (currentQuestion === 41) {
                    showResults();
                } else {
                    currentQuestion++;
                    showQuestion();
                    updateProgress();
                    updateNavigation();
                }
            }
        }
        
        // 결과 계산 및 표시
        function showResults() {
            const result = calculateResult();
            displayResults(result);
            
            testContainer.style.display = 'none';
            results.style.display = 'block';
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
        
        // 결과 계산
        function calculateResult() {
            const dimensionScores = [];
            
            for (let d = 0; d < 7; d++) {
                let sum = 0;
                for (let q = 0; q < 6; q++) {
                    sum += answers[d * 6 + q];
                }
                
                let typeIndex;
                if (sum >= 6 && sum <= 9) typeIndex = 0;
                else if (sum >= 10 && sum <= 12) typeIndex = 1;
                else if (sum >= 13 && sum <= 15) typeIndex = 2;
                else typeIndex = 3;
                
                dimensionScores.push({
                    name: dimensions[d].name,
                    code: dimensions[d].codes[typeIndex],
                    description: dimensions[d].descriptions[typeIndex],
                    score: sum
                });
            }
            
            return dimensionScores;
        }
        
        // 결과 표시
        function displayResults(result) {
            // 성격 유형 코드 생성
            const typeCode = result.map(d => d.code).join('');
            document.getElementById('resultType').textContent = typeCode;
            document.getElementById('resultTitle').textContent = getPersonalityTitle(typeCode);
            
            // 차원별 결과 표시
            const dimensionsGrid = document.getElementById('dimensionsGrid');
            dimensionsGrid.innerHTML = '';
            
            result.forEach(dimension => {
                const dimElement = document.createElement('div');
                dimElement.className = 'dimension-result';
                dimElement.innerHTML = `
                    <div class="dimension-name">${dimension.name}</div>
                    <div class="dimension-value">${dimension.code}</div>
                    <div class="dimension-desc">${dimension.description}</div>
                `;
                dimensionsGrid.appendChild(dimElement);
            });
            
            // 호환성 표시
            displayCompatibility(typeCode);
            
            // 직업 추천 표시
            displayJobs(typeCode);
        }
        
        // 성격 유형 제목 생성
        function getPersonalityTitle(typeCode) {
            const titles = {
                'AEJNR11': 'CEO형',
                'AHJNR42': '혁신 리더형',
                'BFKNR33': '협력 리더형',
                'DEJNR22': '과학자형',
                'CGJOR33': '창의 전문가형',
                'CGLOR34': '상담 전문가형',
                'DHLPT14': '예술가형',
                'AGKOR43': '디자이너형',
                'AGLOR44': '엔터테이너형',
                'BFKOR34': '중재자형',
                'CFMNR24': '서포터형',
                'AEMNR23': '팀워커형',
                'AEMNR13': '실무자형',
                'AHIOR41': '도전자형',
                'DEMNQ12': '장인형'
            };
            
            return titles[typeCode] || '균형잡힌 다면형';
        }
        
        // 호환성 표시
        function displayCompatibility(typeCode) {
            const compatibilityGrid = document.getElementById('compatibilityGrid');
            compatibilityGrid.innerHTML = '';
            
            const compatibility = getCompatibility(typeCode);
            
            compatibility.forEach(comp => {
                const compElement = document.createElement('div');
                compElement.className = 'compatibility-item';
                compElement.innerHTML = `
                    <div class="compatibility-type">${comp.type}</div>
                    <div class="compatibility-desc">${comp.description}</div>
                `;
                compatibilityGrid.appendChild(compElement);
            });
        }
        
        // 호환성 데이터
        function getCompatibility(typeCode) {
            // 간단한 호환성 규칙 (실제로는 더 복잡한 알고리즘 필요)
            const firstChar = typeCode[0];
            const compatibility = [];
            
            if (firstChar === 'A' || firstChar === 'B') {
                compatibility.push({
                    type: 'CFMNR24 (서포터형)',
                    description: '서로 보완하는 완벽한 조합'
                });
            }
            
            if (typeCode.includes('3') && typeCode.includes('4')) {
                compatibility.push({
                    type: 'BFKNR33 (협력 리더형)',
                    description: '공통의 협력적 성향으로 조화로운 관계'
                });
            }
            
            compatibility.push({
                type: typeCode,
                description: '같은 유형끼리는 서로를 잘 이해함'
            });
            
            return compatibility;
        }
        
        // 직업 추천 표시
        function displayJobs(typeCode) {
            const jobGrid = document.getElementById('jobGrid');
            jobGrid.innerHTML = '';
            
            const jobs = getRecommendedJobs(typeCode);
            
            jobs.forEach(job => {
                const jobElement = document.createElement('div');
                jobElement.className = 'job-item';
                jobElement.innerHTML = `
                    <div class="job-title">${job.title}</div>
                    <div class="job-match">${job.match}% 매칭</div>
                `;
                jobGrid.appendChild(jobElement);
            });
        }
        
        // 직업 추천 데이터
        function getRecommendedJobs(typeCode) {
            const jobDatabase = {
                'A': [
                    { title: 'CEO/임원', match: 95 },
                    { title: '영업 관리자', match: 90 },
                    { title: '마케팅 매니저', match: 85 },
                    { title: '프로젝트 매니저', match: 80 }
                ],
                'B': [
                    { title: '팀 리더', match: 90 },
                    { title: 'HR 매니저', match: 85 },
                    { title: '컨설턴트', match: 80 },
                    { title: '교육 전문가', match: 75 }
                ],
                'C': [
                    { title: '상담사', match: 90 },
                    { title: '심리치료사', match: 85 },
                    { title: '사회복지사', match: 80 },
                    { title: '코치', match: 75 }
                ],
                'D': [
                    { title: '연구원', match: 95 },
                    { title: '과학자', match: 90 },
                    { title: '개발자', match: 85 },
                    { title: '분석가', match: 80 }
                ]
            };
            
            const firstChar = typeCode[0];
            return jobDatabase[firstChar] || [
                { title: '다양한 분야 적합', match: 80 },
                { title: '균형잡힌 역할', match: 75 },
                { title: '팀 조율자', match: 70 },
                { title: '다재다능한 포지션', match: 65 }
            ];
        }
        
        // 테스트 재시작
        function restartTest() {
            testContainer.style.display = 'block';
            results.style.display = 'none';
            initTest();
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
        
        // 키보드 이벤트
        document.addEventListener('keydown', (e) => {
            if (testContainer.style.display !== 'none') {
                if (e.key >= '1' && e.key <= '4') {
                    const index = parseInt(e.key) - 1;
                    options[index].click();
                } else if (e.key === 'Enter' && !nextBtn.disabled) {
                    nextQuestion();
                } else if (e.key === 'Backspace' && currentQuestion > 0) {
                    prevQuestion();
                }
            }
        });
        
        // 초기화
        initTest();
    </script>
</body>
</html>
