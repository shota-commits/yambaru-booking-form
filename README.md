<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>やんばるの森 ネイチャーガイド 予約フォーム</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&family=Noto+Sans+JP:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', 'Noto Sans JP', sans-serif;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }
        .modal-backdrop {
            transition: opacity 0.3s ease-in-out;
        }
        .loader {
            border-top-color: #3498db;
            -webkit-animation: spinner 1.5s linear infinite;
            animation: spinner 1.5s linear infinite;
        }
        @keyframes spinner {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        /* AI提案機能の表示・非表示アニメーション */
        .ai-feature-container {
            transition: all 0.5s ease-in-out;
            max-height: 0;
            overflow: hidden;
            opacity: 0;
        }
        .ai-feature-container.visible {
            max-height: 1000px; /* 十分な高さを確保 */
            opacity: 1;
            margin-top: 1.5rem; /* 24px */
        }
    </style>
</head>
<body class="bg-gray-100">

    <div class="container mx-auto p-4 sm:p-8 max-w-4xl">
        
        <header class="text-center mb-8">
            <h1 class="text-3xl sm:text-4xl font-bold text-green-800">やんばるの森 ネイチャーガイド</h1>
            <p class="text-gray-600 mt-2">ご予約・お問い合わせフォーム</p>
        </header>

        <div class="bg-white rounded-2xl shadow-lg overflow-hidden">
            <div class="p-8 sm:p-12">
                <p class="text-gray-700 mb-6">
                    以下のフォームに必要事項をご記入の上、送信してください。
                    内容を確認後、担当者より折り返しご連絡いたします。
                </p>

                <form id="bookingForm" action="https://formspree.io/f/mrblqyzy" method="POST">
                    <div class="space-y-6">
                        <!-- Tour Selection -->
                        <div>
                            <label for="tour" class="block text-sm font-medium text-gray-800 mb-1">ご希望のツアー <span class="text-red-500">*</span></label>
                            <select id="tour" name="tour" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-green-500 transition bg-white">
                                <option value="" disabled selected>ツアーを選択してください</option>
                                <option value="やんばるの森ハイキング">やんばるの森ハイキング</option>
                                <option value="ナイトツアー">ナイトツアー</option>
                                <option value="リバートレッキング">リバートレッキング</option>
                                <option value="オーダーメイドツアー">オーダーメイドツアー</option>
                            </select>
                        </div>

                        <!-- Other form fields -->
                        <div>
                            <label for="name" class="block text-sm font-medium text-gray-800 mb-1">お名前 <span class="text-red-500">*</span></label>
                            <input type="text" id="name" name="name" placeholder="例：山田 太郎" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-green-500 transition">
                        </div>
                        <div>
                            <label for="furigana" class="block text-sm font-medium text-gray-800 mb-1">フリガナ <span class="text-red-500">*</span></label>
                            <input type="text" id="furigana" name="furigana" placeholder="例：ヤマダ タロウ" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-green-500 transition">
                        </div>
                        <div>
                            <label for="email" class="block text-sm font-medium text-gray-800 mb-1">メールアドレス <span class="text-red-500">*</span></label>
                            <input type="email" id="email" name="email" placeholder="例：example@email.com" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-green-500 transition">
                        </div>
                        <div>
                            <label for="phone" class="block text-sm font-medium text-gray-800 mb-1">電話番号 <span class="text-red-500">*</span></label>
                            <input type="tel" id="phone" name="phone" placeholder="例：090-1234-5678" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-green-500 transition">
                        </div>
                        <div>
                            <label for="date" class="block text-sm font-medium text-gray-800 mb-1">ご希望の日時 <span class="text-red-500">*</span></label>
                            <input type="date" id="date" name="date" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-green-500 transition">
                        </div>
                        <div>
                            <label for="participants" class="block text-sm font-medium text-gray-800 mb-1">参加人数 <span class="text-red-500">*</span></label>
                            <input type="number" id="participants" name="participants" min="1" placeholder="例：2" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-green-500 transition">
                        </div>
                        
                        <!-- Message / Custom Request -->
                        <div>
                            <label for="message" class="block text-sm font-medium text-gray-800 mb-1">お問い合わせ内容・ご要望</label>
                            <textarea id="message" name="message" rows="4" placeholder="お子様の年齢、体力に関するご相談、特定の動植物への興味など、ご自由にお書きください。" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-green-500 transition"></textarea>
                        </div>
                        
                        <!-- ★★ Gemini API Feature Container ★★ -->
                        <div id="aiFeatureContainer" class="ai-feature-container">
                            <p class="text-sm text-gray-600 mb-2">「オーダーメイドツアー」をご希望の方へ。ご要望を上記にご記入の上、AIに旅程の提案を依頼できます。</p>
                            <button type="button" id="generatePlanButton" class="w-full sm:w-auto bg-orange-500 hover:bg-orange-600 text-white font-bold py-2 px-6 rounded-lg shadow-md hover:shadow-lg transition-all duration-300">
                                ✨ AIに旅程の提案を依頼する
                            </button>
                            <div id="aiPlanResult" class="mt-4 p-4 border border-green-200 rounded-lg bg-green-50 hidden">
                                <!-- AI generated plan will be inserted here -->
                            </div>
                        </div>
                    </div>

                    <!-- Submit Button -->
                    <div class="mt-8 text-center">
                        <button type="submit" id="submitButton" class="w-full sm:w-auto bg-green-700 hover:bg-green-800 text-white font-bold py-3 px-12 rounded-full shadow-lg transform hover:scale-105 transition-all duration-300 ease-in-out">
                            予約内容を送信する
                        </button>
                    </div>
                </form>
            </div>
        </div>
        
        <footer class="text-center mt-8 text-sm text-gray-500">
            <p>&copy; 2025 やんばるの森 ネイチャーガイド. All Rights Reserved.</p>
        </footer>
    </div>

    <!-- Modals (Success, Error) -->
    <div id="successModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50 opacity-0 pointer-events-none modal-backdrop">
        <div class="bg-white rounded-2xl shadow-xl p-8 max-w-sm w-full text-center transform scale-95 transition-transform duration-300 ease-in-out">
            <div class="mx-auto flex items-center justify-center h-16 w-16 rounded-full bg-green-100 mb-4">
                <svg class="h-10 w-10 text-green-600" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" /></svg>
            </div>
            <h3 class="text-xl font-semibold text-gray-900 mb-2">送信完了</h3>
            <p class="text-gray-600 mb-6">お問い合わせいただきありがとうございます。<br>内容を確認の上、3営業日以内にご指定のメールアドレスへ返信いたします。</p>
            <button id="closeModal" class="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded-lg transition">閉じる</button>
        </div>
    </div>
    <div id="errorModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50 opacity-0 pointer-events-none modal-backdrop">
        <div class="bg-white rounded-2xl shadow-xl p-8 max-w-sm w-full text-center transform scale-95 transition-transform duration-300 ease-in-out">
             <div class="mx-auto flex items-center justify-center h-16 w-16 rounded-full bg-red-100 mb-4">
                <svg class="h-10 w-10 text-red-600" stroke="currentColor" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
            </div>
            <h3 class="text-xl font-semibold text-gray-900 mb-2">送信エラー</h3>
            <p class="text-gray-600 mb-6">申し訳ありません。メッセージの送信に失敗しました。<br>時間をおいて再度お試しください。</p>
            <button id="closeErrorModal" class="w-full bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg transition">閉じる</button>
        </div>
    </div>

    <script>
        const bookingForm = document.getElementById('bookingForm');
        const submitButton = document.getElementById('submitButton');
        const successModal = document.getElementById('successModal');
        const errorModal = document.getElementById('errorModal');
        const closeModalButton = document.getElementById('closeModal');
        const closeErrorModalButton = document.getElementById('closeErrorModal');
        
        // ★★ Gemini API Feature Elements ★★
        const tourSelect = document.getElementById('tour');
        const aiFeatureContainer = document.getElementById('aiFeatureContainer');
        const generatePlanButton = document.getElementById('generatePlanButton');
        const aiPlanResult = document.getElementById('aiPlanResult');
        const messageTextarea = document.getElementById('message');

        // Show/hide AI feature based on tour selection
        tourSelect.addEventListener('change', () => {
            if (tourSelect.value === 'オーダーメイドツアー') {
                aiFeatureContainer.classList.add('visible');
            } else {
                aiFeatureContainer.classList.remove('visible');
                aiPlanResult.classList.add('hidden');
                aiPlanResult.innerHTML = '';
            }
        });

        // ★★ Gemini API Call Logic ★★
        generatePlanButton.addEventListener('click', async () => {
            const userRequest = messageTextarea.value;
            if (!userRequest.trim()) {
                alert('「お問い合わせ内容・ご要望」に、どのようなツアーにしたいかご記入ください。');
                return;
            }

            // Show loading state
            generatePlanButton.disabled = true;
            generatePlanButton.innerHTML = '<div class="loader ease-linear rounded-full border-2 border-t-2 border-gray-200 h-5 w-5 mx-auto"></div>';
            aiPlanResult.classList.remove('hidden');
            aiPlanResult.innerHTML = '<p class="text-center text-gray-600">AIがあなただけのプランを考えています...</p>';

            const prompt = `あなたは沖縄の「やんばるの森」を専門とする非常に優秀でフレンドリーなネイチャーガイドです。以下の顧客の要望に基づいて、魅力的で具体的な半日（約3〜4時間）のオーダーメイドツアーの旅程を提案してください。提案には、具体的な場所の候補、おおよその時間配分、見どころ、そしてなぜそのプランがお客様におすすめなのかを、情熱を込めて説明してください。安全に関する注意点ももしあれば含めてください。箇条書きなどを用いて、分かりやすく楽しい雰囲気で出力してください。\n\n# 顧客の要望:\n${userRequest}`;

            try {
                let chatHistory = [];
                chatHistory.push({ role: "user", parts: [{ text: prompt }] });
                const payload = { contents: chatHistory };
                const apiKey = ""; 
                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;
                
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });

                if (!response.ok) {
                    throw new Error(`API Error: ${response.statusText}`);
                }

                const result = await response.json();
                
                if (result.candidates && result.candidates.length > 0 && result.candidates[0].content && result.candidates[0].content.parts && result.candidates[0].content.parts.length > 0) {
                    const text = result.candidates[0].content.parts[0].text;
                    // Format the response with line breaks
                    aiPlanResult.innerHTML = `<h4 class="font-bold text-lg text-green-800 mb-2">AIからのツアープラン提案</h4><div class="prose prose-sm max-w-none">${text.replace(/\n/g, '<br>')}</div>`;
                } else {
                    throw new Error('AIからの応答がありませんでした。');
                }

            } catch (error) {
                console.error('Gemini API Error:', error);
                aiPlanResult.innerHTML = '<p class="text-center text-red-600">プランの生成に失敗しました。時間をおいて再度お試しください。</p>';
            } finally {
                // Restore button
                generatePlanButton.disabled = false;
                generatePlanButton.innerHTML = '✨ AIに旅程の提案を依頼する';
            }
        });


        // Formspree submission logic
        bookingForm.addEventListener('submit', function(event) {
            event.preventDefault();

            const formData = new FormData(bookingForm);
            // Append AI plan to form data if it exists
            if (!aiPlanResult.classList.contains('hidden') && aiPlanResult.innerText.trim() !== '') {
                formData.append('ai_suggested_plan', aiPlanResult.innerText);
            }
            const action = bookingForm.getAttribute('action');
            
            submitButton.disabled = true;
            submitButton.innerHTML = '<div class="loader ease-linear rounded-full border-4 border-t-4 border-gray-200 h-6 w-6 mx-auto"></div>';

            fetch(action, {
                method: 'POST',
                body: formData,
                headers: { 'Accept': 'application/json' }
            }).then(response => {
                if (response.ok) {
                    showModal(successModal);
                    bookingForm.reset();
                    aiFeatureContainer.classList.remove('visible');
                    aiPlanResult.classList.add('hidden');
                    aiPlanResult.innerHTML = '';
                } else {
                    response.json().then(data => {
                        if (Object.hasOwn(data, 'errors')) {
                            alert(data["errors"].map(error => error["message"]).join(", "));
                        }
                        showModal(errorModal);
                    })
                }
            }).catch(error => {
                showModal(errorModal);
            }).finally(() => {
                submitButton.disabled = false;
                submitButton.innerHTML = '予約内容を送信する';
            });
        });

        // Modal handling functions
        function showModal(modal) {
            const modalContent = modal.querySelector('div');
            modal.classList.remove('opacity-0', 'pointer-events-none');
            modalContent.classList.remove('scale-95');
        }

        function closeModal(modal) {
            const modalContent = modal.querySelector('div');
            modalContent.classList.add('scale-95');
            modal.classList.add('opacity-0');
            setTimeout(() => {
                modal.classList.add('pointer-events-none');
            }, 300);
        }

        closeModalButton.addEventListener('click', () => closeModal(successModal));
        closeErrorModalButton.addEventListener('click', () => closeModal(errorModal));

        document.addEventListener('keydown', function(event) {
            if (event.key === 'Escape') {
                if (!successModal.classList.contains('pointer-events-none')) closeModal(successModal);
                if (!errorModal.classList.contains('pointer-events-none')) closeModal(errorModal);
            }
        });
    </script>
</body>
</html>
