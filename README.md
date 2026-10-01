<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>แบบประเมินความรู้สึก (Pre/Post Test)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Prompt', sans-serif; background-color: #f3f4f6; }
        .fade-in { animation: fadeIn 0.4s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body class="text-gray-800 p-4 md:p-8">

    <div class="max-w-3xl mx-auto bg-white rounded-2xl shadow-lg overflow-hidden fade-in">
        <div class="bg-blue-600 text-white p-6 text-center">
            <h1 class="text-2xl font-semibold">แบบประเมินสภาวะอารมณ์และความรู้สึก</h1>
            <p class="text-sm mt-2 opacity-90">เพื่อประเมินผลก่อนและหลังการเข้าร่วมกิจกรรม</p>
        </div>

        <form id="assessmentForm" class="p-6 md:p-8">
            
            <!-- Step 1: ข้อมูลส่วนตัว -->
            <div id="step1">
                <h2 class="text-xl font-medium text-blue-700 border-b pb-2 mb-6">ส่วนที่ 1: ข้อมูลทั่วไป</h2>
                
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                    <div>
                        <label class="block text-sm font-medium mb-1">รหัสนักศึกษา (ถ้ามี)</label>
                        <input type="text" id="studentId" class="w-full border rounded-lg p-2 focus:ring-2 focus:ring-blue-500 outline-none" placeholder="เช่น B6XXXXX">
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-1">ระยะการประเมิน *</label>
                        <select id="testPhase" required class="w-full border rounded-lg p-2 focus:ring-2 focus:ring-blue-500 outline-none">
                            <option value="">-- กรุณาเลือก --</option>
                            <option value="Pre-test">ก่อนเข้าร่วมกิจกรรม (Pre-test)</option>
                            <option value="Post-test">หลังเข้าร่วมกิจกรรม (Post-test)</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-1">เพศ *</label>
                        <select id="gender" required class="w-full border rounded-lg p-2 focus:ring-2 focus:ring-blue-500 outline-none">
                            <option value="">-- กรุณาเลือก --</option>
                            <option value="ชาย">ชาย</option>
                            <option value="หญิง">หญิง</option>
                            <option value="อื่นๆ">อื่นๆ / ไม่ระบุ</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium mb-1">ชั้นปี *</label>
                        <select id="year" required class="w-full border rounded-lg p-2 focus:ring-2 focus:ring-blue-500 outline-none">
                            <option value="">-- กรุณาเลือก --</option>
                            <option value="ปี 1">ปี 1</option>
                            <option value="ปี 2">ปี 2</option>
                            <option value="ปี 3">ปี 3</option>
                            <option value="ปี 4">ปี 4</option>
                            <option value="อื่นๆ">อื่นๆ</option>
                        </select>
                    </div>
                    <div class="md:col-span-2">
                        <label class="block text-sm font-medium mb-1">สถานที่ / คณะ / สาขาที่สังกัด *</label>
                        <input type="text" id="location" required class="w-full border rounded-lg p-2 focus:ring-2 focus:ring-blue-500 outline-none" placeholder="โปรดระบุข้อมูล">
                    </div>
                </div>
                
                <div class="text-right">
                    <button type="button" onclick="nextStep()" class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-6 rounded-lg transition">ถัดไป ➔</button>
                </div>
            </div>

            <!-- Step 2: แบบประเมิน -->
            <div id="step2" class="hidden fade-in">
                <h2 class="text-xl font-medium text-blue-700 border-b pb-2 mb-6">ส่วนที่ 2: แบบประเมินความรู้สึก</h2>
                <p class="text-sm text-gray-500 mb-4">โปรดเลือกระดับความรู้สึกที่ตรงกับคุณมากที่สุดในขณะนี้ (5 = มากที่สุด, 1 = น้อยที่สุด)</p>
                
                <div id="questionsContainer" class="space-y-6">
                    <!-- คำถามจะถูกสร้างด้วย JavaScript -->
                </div>

                <div class="flex justify-between mt-8">
                    <button type="button" onclick="prevStep()" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-medium py-2 px-6 rounded-lg transition">⬅ ย้อนกลับ</button>
                    <button type="submit" class="bg-green-600 hover:bg-green-700 text-white font-medium py-2 px-6 rounded-lg shadow-lg transition">ส่งผลการประเมิน</button>
                </div>
            </div>

        </form>
    </div>

    <!-- Modal แสดงผลลัพธ์ -->
    <div id="resultModal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50 fade-in">
        <div class="bg-white rounded-2xl p-8 max-w-md w-full mx-4 text-center shadow-2xl relative">
            <div id="modalIcon" class="text-6xl mb-4">✨</div>
            <h3 class="text-2xl font-semibold mb-2" id="modalLevel">ระดับดีเยี่ยม</h3>
            <p class="text-gray-600 mb-6" id="modalRecommendation">คำแนะนำจะแสดงที่นี่...</p>
            
            <div class="p-4 bg-gray-50 rounded-lg text-sm text-left mb-6 text-gray-500">
                <p>✓ บันทึกข้อมูลเข้าสู่ระบบเรียบร้อยแล้ว</p>
                <p id="summaryInfo">รหัส: - | รอบ: -</p>
            </div>

            <button onclick="closeModal()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-medium py-3 rounded-lg transition">
                กลับสู่หน้าเริ่มต้น
            </button>
        </div>
    </div>

    <script>
        const questions = [
            { id: 'q1', text: '1. ฉันรู้สึกมีความสุขและสนุกสนาน', type: 'positive' },
            { id: 'q2', text: '2. ฉันรู้สึกผ่อนคลาย ไม่กดดัน', type: 'positive' },
            { id: 'q3', text: '3. ฉันรู้สึกกระตือรือร้นและมีพลังงาน', type: 'positive' },
            { id: 'q4', text: '4. ฉันรู้สึกมีสมาธิและจดจ่อกับสิ่งรอบตัว', type: 'positive' },
            { id: 'q5', text: '5. ฉันรู้สึกได้รับแรงบันดาลใจ/มีมุมมองเชิงบวก', type: 'positive' },
            { id: 'q6', text: '6. ฉันรู้สึกเครียด หรือวิตกกังวล', type: 'negative' },
            { id: 'q7', text: '7. ฉันรู้สึกเบื่อหน่าย ไม่อยากมีส่วนร่วม', type: 'negative' },
            { id: 'q8', text: '8. ฉันรู้สึกเหนื่อยล้า อ่อนเพลีย', type: 'negative' }
        ];

        const container = document.getElementById('questionsContainer');

        questions.forEach((q) => {
            const html = `
                <div class="bg-gray-50 p-4 rounded-lg border border-gray-100">
                    <p class="mb-3 font-medium text-gray-700">${q.text}</p>
                    <div class="flex justify-between max-w-md mx-auto">
                        ${[1, 2, 3, 4, 5].map(val => `
                            <label class="flex flex-col items-center cursor-pointer group">
                                <input type="radio" name="${q.id}" value="${val}" required class="w-5 h-5 text-blue-600 mb-1 cursor-pointer">
                                <span class="text-xs text-gray-400 group-hover:text-blue-600">${val}</span>
                            </label>
                        `).join('')}
                    </div>
                </div>
            `;
            container.insertAdjacentHTML('beforeend', html);
        });

        function nextStep() {
            const requiredFields = ['testPhase', 'gender', 'year', 'location'];
            const isValid = requiredFields.every(id => {
                const element = document.getElementById(id);
                return element && element.value && element.value.trim() !== '';
            });

            if (!isValid) {
                alert('กรุณากรอกข้อมูลที่มีเครื่องหมาย * ให้ครบถ้วน');
                return;
            }

            document.getElementById('step1').classList.add('hidden');
            document.getElementById('step2').classList.remove('hidden');
        }

        function prevStep() {
            document.getElementById('step2').classList.add('hidden');
            document.getElementById('step1').classList.remove('hidden');
        }

        function getSelectedValue(questionId) {
            const selected = document.querySelector(`input[name="${questionId}"]:checked`);
            return selected ? Number(selected.value) : null;
        }

        document.getElementById('assessmentForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const unansweredQuestions = questions.filter(q => getSelectedValue(q.id) === null);
            if (unansweredQuestions.length > 0) {
                alert('กรุณาเลือกคำตอบให้ครบทุกข้อก่อนส่งผลการประเมิน');
                return;
            }

            const formData = {
                studentId: document.getElementById('studentId').value.trim() || 'ไม่ระบุ',
                testPhase: document.getElementById('testPhase').value,
                gender: document.getElementById('gender').value,
                year: document.getElementById('year').value,
                location: document.getElementById('location').value.trim(),
                timestamp: new Date().toLocaleString('th-TH')
            };

            let totalScore = 0;
            questions.forEach(q => {
                const value = getSelectedValue(q.id);
                formData[q.id] = value;

                let score = value;
                if (q.type === 'negative') {
                    score = 6 - value;
                }
                totalScore += score;
            });

            let level, recommendation, icon, colorClass;

            if (totalScore >= 33) {
                level = 'ดีเยี่ยม';
                recommendation = 'สภาวะอารมณ์ของคุณอยู่ในเกณฑ์ดีเยี่ยม มีพลังบวกและพร้อมเรียนรู้หรือทำกิจกรรมต่างๆ ขอให้รัก��าความรู้สึกที่ดีนี้ไว้ต่อไปครับ';
                icon = '🌟';
                colorClass = 'text-green-600';
            } else if (totalScore >= 26) {
                level = 'ดีมาก';
                recommendation = 'คุณสามารถจัดการอารมณ์ได้ดี มีความพร้อมในระดับที่ดี หากมีเรื่องท้าทายก็สามารถรับมือได้อย่างสบาย';
                icon = '😊';
                colorClass = 'text-blue-500';
            } else if (totalScore >= 19) {
                level = 'ปานกลาง';
                recommendation = 'อารมณ์ของคุณอยู่ในเกณฑ์ปกติ อาจมีเหนื่อยล้าหรือเบื่อบ้างเล็กน้อย แนะนำให้หาเวลาพักสายตาหรือทำกิจกรรมที่ผ่อนคลายระหว่างวัน';
                icon = '😌';
                colorClass = 'text-yellow-500';
            } else if (totalScore >= 12) {
                level = 'เริ่มมีภาวะตึงเครียด';
                recommendation = 'คุณอาจกำลังรู้สึกเหนื่อยล้าหรือมีเรื่องให้คิดมาก แนะนำให้ลดความคาดหวังลงชั่วคราว หาเวลาพักผ่อนอย่างจริงจัง หรือพูดคุยระบายกับคนใกล้ชิด';
                icon = '😟';
                colorClass = 'text-orange-500';
            } else {
                level = 'ภาวะเสี่ยง (ควรได้รับการดูแล)';
                recommendation = 'สภาวะอารมณ์ของคุณค่อนข้างเปราะบางและมีความตึงเครียดสูงมาก ขอแนะนำให้คุณพักผ่อนทันที หากรู้สึกไม่ดีขึ้น ควรพิจารณาปรึกษาผู้เชี่ยวชาญหรือศูนย์ให้คำปรึกษาของสถานศึกษาครับ';
                icon = '❤️‍🩹';
                colorClass = 'text-red-600';
            }

            formData.resultLevel = level;

            document.getElementById('modalIcon').textContent = icon;
            document.getElementById('modalLevel').textContent = 'ระดับ: ' + level;
            document.getElementById('modalLevel').className = 'text-2xl font-semibold mb-2 ' + colorClass;
            document.getElementById('modalRecommendation').textContent = recommendation;
            document.getElementById('summaryInfo').textContent = `รหัส: ${formData.studentId} | รอบ: ${formData.testPhase}`;
            document.getElementById('resultModal').classList.remove('hidden');

            sendDataToGoogleSheets(formData);
        });

        function sendDataToGoogleSheets(data) {
            const scriptURL = 'https://script.google.com/macros/s/AKfycbzy3pqqo8D0d_Lzy7myqK0DF_wwn5OdRi0W52delCRutSI3qlvEIj3VIoUOb6jltKsI_Q/exec';

            console.log('ข้อมูลที่เตรียมส่งเข้า Sheet:', data);

            fetch(scriptURL, {
                method: 'POST',
                body: JSON.stringify(data),
                headers: { 'Content-Type': 'text/plain;charset=utf-8' }
            })
            .then(() => console.log('ส่งข้อมูลสำเร็จ'))
            .catch(error => console.error('เกิดข้อผิดพลาดในการส่งข้อมูล:', error.message));
        }

        function closeModal() {
            document.getElementById('resultModal').classList.add('hidden');
            document.getElementById('assessmentForm').reset();
            document.getElementById('step2').classList.add('hidden');
            document.getElementById('step1').classList.remove('hidden');
        }
    </script>
</body>
</html>
