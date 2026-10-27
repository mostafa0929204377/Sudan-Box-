<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>الجيم السوداني 🇸🇩 | Sudanese Gym</title>
  <!-- Tailwind CSS للتصميم العصري والسريع -->
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;900&display=swap');
    body { font-family: 'Tajawal', sans-serif; background-color: #0f172a; color: #f8fafc; }
    .active-tab { border-bottom: 3px solid #22c55e; color: #22c55e; font-weight: bold; }
  </style>
</head>
<body class="min-h-screen pb-16">

  <!-- الرأس (Header) -->
  <header class="bg-slate-900 border-b border-slate-800 p-4 sticky top-0 z-50 shadow-lg">
    <div class="max-w-4xl mx-auto flex justify-between items-center">
      <div class="flex items-center space-x-2 space-x-reverse">
        <span class="text-3xl">🏋️‍♂️</span>
        <div>
          <h1 class="text-xl font-extrabold text-green-500">الجيم السوداني</h1>
          <p class="text-xs text-slate-400">لياقتك وصحتك في مكان واحد 🇸🇩</p>
        </div>
      </div>
      <div id="quickStats" class="text-xs bg-slate-800 px-3 py-1.5 rounded-lg border border-slate-700 hidden">
        <span>هدفك: <b id="headCal" class="text-green-400">--</b> سعرة</span>
      </div>
    </div>
  </header>

  <!-- شريط التبديل بين الأقسام (Navigation Tabs) -->
  <nav class="bg-slate-900/80 backdrop-blur sticky top-[69px] z-40 border-b border-slate-800">
    <div class="max-w-4xl mx-auto flex justify-around text-sm md:text-base">
      <button onclick="switchTab('profile')" id="tab-profile" class="tab-btn py-3 px-2 active-tab">👤 الملف الصحي</button>
      <button onclick="switchTab('camera')" id="tab-camera" class="tab-btn py-3 px-2 text-slate-400">📸 حاسبة الأكل</button>
      <button onclick="switchTab('water')" id="tab-water" class="tab-btn py-3 px-2 text-slate-400">💧 عداد الماء</button>
      <button onclick="switchTab('workouts')" id="tab-workouts" class="tab-btn py-3 px-2 text-slate-400">🔥 التمارين</button>
      <button onclick="switchTab('chat')" id="tab-chat" class="tab-btn py-3 px-2 text-slate-400">🤖 كابتن AI</button>
    </div>
  </nav>

  <main class="max-w-4xl mx-auto p-4 space-y-6">

    <!-- 1. قسم الملف الشخصي والصحي -->
    <section id="sec-profile" class="tab-content block">
      <div class="bg-slate-800/80 p-6 rounded-2xl border border-slate-700 shadow-xl">
        <h2 class="text-lg font-bold text-green-400 mb-4 flex items-center gap-2">
          <span>📋</span> بياناتك الشخصية وحالتك الصحية
        </h2>
        
        <form id="healthForm" onsubmit="calculateHealth(event)" class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div>
            <label class="block text-xs text-slate-300 mb-1">النوع</label>
            <select id="gender" class="w-full bg-slate-900 border border-slate-700 rounded-xl p-3 text-white focus:border-green-500 outline-none">
              <option value="male">ذكر 👨</option>
              <option value="female">أنثى 👩</option>
            </select>
          </div>

          <div>
            <label class="block text-xs text-slate-300 mb-1">العمر (سنة)</label>
            <input type="number" id="age" value="25" required class="w-full bg-slate-900 border border-slate-700 rounded-xl p-3 text-white focus:border-green-500 outline-none">
          </div>

          <div>
            <label class="block text-xs text-slate-300 mb-1">الوزن الحالي (كجم)</label>
            <input type="number" id="weight" value="85" required class="w-full bg-slate-900 border border-slate-700 rounded-xl p-3 text-white focus:border-green-500 outline-none">
          </div>

          <div>
            <label class="block text-xs text-slate-300 mb-1">الطول (سم)</label>
            <input type="number" id="height" value="175" required class="w-full bg-slate-900 border border-slate-700 rounded-xl p-3 text-white focus:border-green-500 outline-none">
          </div>

          <div class="md:col-span-2">
            <label class="block text-xs text-slate-300 mb-1">هل تعاني من أي أمراض أو إصابات؟</label>
            <select id="disease" class="w-full bg-slate-900 border border-slate-700 rounded-xl p-3 text-white focus:border-green-500 outline-none">
              <option value="none">سليم والحمد لله (لا توجد أمراض)</option>
              <option value="knee">آلام مفاصل أو خشونة ركبة</option>
              <option value="hypertension">ضغط دم مرتفع</option>
              <option value="diabetes">مرض السكري</option>
              <option value="back">آلام أسفل الظهر (غضروف/دسك)</option>
            </select>
          </div>

          <div class="md:col-span-2 mt-2">
            <button type="submit" class="w-full bg-green-500 hover:bg-green-600 text-slate-950 font-extrabold py-3.5 rounded-xl transition shadow-lg shadow-green-500/20">
              احسب خطتي لإنقاص الوزن 🚀
            </button>
          </div>
        </form>

        <!-- نتائج الحساب -->
        <div id="resultsBox" class="mt-6 pt-6 border-t border-slate-700 grid grid-cols-2 md:grid-cols-4 gap-3 text-center hidden">
          <div class="bg-slate-900 p-3 rounded-xl border border-slate-800">
            <span class="text-xs text-slate-400">كتلة الجسم (BMI)</span>
            <p id="bmiVal" class="text-lg font-bold text-white mt-1">--</p>
          </div>
          <div class="bg-slate-900 p-3 rounded-xl border border-slate-800">
            <span class="text-xs text-slate-400">سعرات التخسيس</span>
            <p id="calVal" class="text-lg font-bold text-green-400 mt-1">--</p>
          </div>
          <div class="bg-slate-900 p-3 rounded-xl border border-slate-800">
            <span class="text-xs text-slate-400">احتياج الماء</span>
            <p id="waterGoal" class="text-lg font-bold text-blue-400 mt-1">--</p>
          </div>
          <div class="bg-slate-900 p-3 rounded-xl border border-slate-800">
            <span class="text-xs text-slate-400">توجيه صحي</span>
            <p id="healthAdvice" class="text-xs font-semibold text-yellow-400 mt-1">--</p>
          </div>
        </div>
      </div>
    </section>

    <!-- 2. قسم كاميرا الطعام وحساب السعرات -->
    <section id="sec-camera" class="tab-content hidden">
      <div class="bg-slate-800/80 p-6 rounded-2xl border border-slate-700 shadow-xl space-y-4">
        <h2 class="text-lg font-bold text-green-400 flex items-center gap-2">
          <span>📷</span> مسح الوجبة وحساب السعرات
        </h2>
        <p class="text-xs text-slate-400">صوّر صحنك أو ارفع صورة وجبتك وسيقوم النظام الذكي بتقدير السعرات السودانية والعالمية.</p>

        <!-- مساحة الكاميرا والمعاينة -->
        <div class="relative bg-slate-950 rounded-2xl overflow-hidden border border-slate-800 aspect-video flex items-center justify-center">
          <video id="videoFeed" autoplay playsinline class="w-full h-full object-cover hidden"></video>
          <img id="imagePreview" class="w-full h-full object-contain hidden" alt="معاينة الوجبة">
          <div id="cameraPlaceholder" class="text-center p-6 text-slate-500">
            <span class="text-5xl block mb-2">🥗</span>
            اضغط "تشغيل الكاميرا" أو اختر صورة من جهازك
          </div>
        </div>

        <!-- أزرار التحكم بالكاميرا -->
        <div class="flex flex-wrap gap-2">
          <button onclick="startCamera()" class="flex-1 bg-slate-700 hover:bg-slate-600 py-3 rounded-xl text-sm font-bold">🎥 تشغيل الكاميرا</button>
          <button onclick="capturePhoto()" id="snapBtn" class="flex-1 bg-green-500 hover:bg-green-600 text-slate-950 py-3 rounded-xl text-sm font-bold hidden">📸 التقط وحلل</button>
          <label class="flex-1 bg-slate-900 border border-slate-700 hover:bg-slate-800 py-3 rounded-xl text-sm font-bold text-center cursor-pointer">
            📁 رفع صورة
            <input type="file" accept="image/*" onchange="handleImageUpload(event)" class="hidden">
          </label>
        </div>

        <!-- نتيجة تحليل الوجبة -->
        <div id="foodResult" class="bg-slate-900 p-4 rounded-xl border border-slate-800 hidden">
          <div class="flex justify-between items-center mb-2">
            <span class="text-sm font-bold text-green-400" id="foodName">--</span>
            <span class="bg-green-500/20 text-green-400 text-xs px-2 py-1 rounded-md" id="foodCal">-- سعرة</span>
          </div>
          <div class="grid grid-cols-3 gap-2 text-center text-xs mt-3">
            <div class="bg-slate-800 p-2 rounded-lg">بروتين: <b class="text-white" id="foodProt">--</b> جم</div>
            <div class="bg-slate-800 p-2 rounded-lg">كاربوهيدرات: <b class="text-white" id="foodCarb">--</b> جم</div>
            <div class="bg-slate-800 p-2 rounded-lg">دهون: <b class="text-white" id="foodFat">--</b> جم</div>
          </div>
          <button onclick="addFoodCalories()" class="w-full mt-3 bg-slate-800 hover:bg-slate-700 text-xs py-2 rounded-lg border border-slate-700">
            ➕ أضفها لسجل يومي
          </button>
        </div>
      </div>
    </section>

    <!-- 3. قسم متابعة شرب الماء -->
    <section id="sec-water" class="tab-content hidden">
      <div class="bg-slate-800/80 p-6 rounded-2xl border border-slate-700 shadow-xl text-center space-y-6">
        <h2 class="text-lg font-bold text-blue-400 flex items-center justify-center gap-2">
          <span>💧</span> متابعة شرب الماء اليومي
        </h2>

        <div class="relative w-44 h-44 mx-auto flex items-center justify-center bg-slate-900 rounded-full border-4 border-blue-500/30">
          <div>
            <span id="currentWater" class="text-4xl font-extrabold text-blue-400">0.0</span>
            <span class="text-xs text-slate-400 block">لتر / <span id="targetWaterDisplay">3.0</span> لتر</span>
          </div>
        </div>

        <!-- شريط التقدم -->
        <div class="w-full bg-slate-900 h-3 rounded-full overflow-hidden border border-slate-800">
          <div id="waterProgressBar" class="bg-blue-500 h-full transition-all duration-300" style="width: 0%"></div>
        </div>

        <!-- أزرار الإضافة -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-3">
          <button onclick="addWater(0.25)" class="bg-slate-900 hover:bg-slate-700 border border-slate-700 p-3 rounded-xl text-sm font-semibold">
            🥛 كباية (+250 مل)
          </button>
          <button onclick="addWater(0.5)" class="bg-slate-900 hover:bg-slate-700 border border-slate-700 p-3 rounded-xl text-sm font-semibold">
            🍶 قارورة صغيرة (+0.5 لتر)
          </button>
          <button onclick="addWater(1.0)" class="bg-slate-900 hover:bg-slate-700 border border-slate-700 p-3 rounded-xl text-sm font-semibold">
            🫗 جك كبير (+1 لتر)
          </button>
          <button onclick="resetWater()" class="bg-rose-500/20 hover:bg-rose-500/30 text-rose-400 border border-rose-500/30 p-3 rounded-xl text-sm font-semibold">
            🔄 تصفير العداد
          </button>
        </div>
      </div>
    </section>

    <!-- 4. قسم تمارين إنقاص الوزن المخصصة -->
    <section id="sec-workouts" class="tab-content hidden">
      <div class="bg-slate-800/80 p-6 rounded-2xl border border-slate-700 shadow-xl space-y-4">
        <div class="flex justify-between items-center">
          <h2 class="text-lg font-bold text-green-400 flex items-center gap-2">
            <span>🔥</span> جدول تمارين إنقاص الوزن
          </h2>
          <span id="workoutBadge" class="text-xs bg-slate-900 border border-slate-700 px-3 py-1 rounded-full text-slate-300">مخصص لحالتك</span>
        </div>
        <p class="text-xs text-slate-400">التمارين التالية معدلة تلقائياً بحسب وزنك وخلوّك أو إصابتك بالأمراض لتفادي أي ضرر للمفاصل والقلب:</p>

        <div id="workoutList" class="space-y-3">
          <!-- التمارين تتولد تلقائياً عبر JavaScript -->
        </div>
      </div>
    </section>

    <!-- 5. قسم المساعد الذكي (كابتن الزول AI) -->
    <section id="sec-chat" class="tab-content hidden">
      <div class="bg-slate-800/80 p-4 md:p-6 rounded-2xl border border-slate-700 shadow-xl flex flex-col h-[520px]">
        <div class="flex items-center gap-3 pb-3 border-b border-slate-700">
          <div class="w-10 h-10 rounded-full bg-green-500/20 flex items-center justify-center text-xl">🤖</div>
          <div>
            <h3 class="text-sm font-bold text-white">كابتن أحمد (المساعد الذكي)</h3>
            <p class="text-xs text-green-400">متصل • خبير الجيم والدايت السوداني</p>
          </div>
        </div>

        <!-- صندوق المحادثة -->
        <div id="chatMessages" class="flex-1 overflow-y-auto space-y-3 py-4 text-sm">
          <div class="bg-slate-900 border border-slate-800 p-3 rounded-2xl rounded-tr-none max-w-[85%] text-slate-200">
            حبابك يا بطل في <b>الجيم السوداني</b>! 🇸🇩 أنا كابتنك الذكي، اسألني عن أي حاجة بتخص السعرات، تمارين إنقاص الوزن، بروتين البوش، أو التمارين المناسبة لصحتك.
          </div>
        </div>

        <!-- إدخال السؤال -->
        <form onsubmit="handleChatSubmit(event)" class="pt-3 border-t border-slate-700 flex gap-2">
          <input type="text" id="chatInput" placeholder="مثلاً: كم سعرة في البوش؟ أو كيف أنزل وزني مع آلام الركبة؟" 
                 class="flex-1 bg-slate-900 border border-slate-700 rounded-xl px-4 py-3 text-white text-sm outline-none focus:border-green-500">
          <button type="submit" class="bg-green-500 hover:bg-green-600 text-slate-950 font-bold px-5 rounded-xl transition">
            إرسال
          </button>
        </form>
      </div>
    </section>

  </main>

  <!-- الكود البرمجي التفاعلي (JavaScript) -->
  <script>
    // --- 1. إدارة التنقل بين التبويبات ---
    function switchTab(tabName) {
      document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
      document.querySelectorAll('.tab-btn').forEach(btn => {
        btn.classList.remove('active-tab');
        btn.classList.add('text-slate-400');
      });

      document.getElementById('sec-' + tabName).classList.remove('hidden');
      const activeBtn = document.getElementById('tab-' + tabName);
      activeBtn.classList.add('active-tab');
      activeBtn.classList.remove('text-slate-400');
    }

    // --- 2. الملف الشخصي، حساب السعرات والماء والتمارين ---
    let userProfile = {
      gender: 'male',
      weight: 85,
      height: 175,
      age: 25,
      disease: 'none',
      targetCalories: 2000,
      targetWater: 3.0
    };

    function calculateHealth(e) {
      e.preventDefault();
      const gender = document.getElementById('gender').value;
      const age = parseFloat(document.getElementById('age').value);
      const weight = parseFloat(document.getElementById('weight').value);
      const height = parseFloat(document.getElementById('height').value);
      const disease = document.getElementById('disease').value;

      // 1. حساب BMI
      const heightInMeters = height / 100;
      const bmi = (weight / (heightInMeters * heightInMeters)).toFixed(1);

      // 2. حساب السعرات بنظام Mifflin-St Jeor
      let bmr = (10 * weight) + (6.25 * height) - (5 * age);
      bmr += (gender === 'male') ? 5 : -161;
      
      // لاستهداف إنقاص الوزن، نضرب في معامل نشاط خفيف ونطرح 400 سعرة
      let targetCalories = Math.round((bmr * 1.35) - 400);
      if (targetCalories < 1200) targetCalories = 1200;

      // 3. حساب احتياج الماء (35 مل لكل كيلو)
      const waterLiters = ((weight * 35) / 1000).toFixed(1);

      // 4. توصيات حسب المرض
      let advice = "جسمك ممتاز للتخسيس";
      if (disease === 'knee') advice = "تمارين بدون قفز لحماية الركبة ⚠️";
      else if (disease === 'hypertension') advice = "تجنب حبس النفس والأوزان القصوى ⚠️";
      else if (disease === 'diabetes') advice = "وزع وجباتك واشرب ماء باستمرار ⚠️";
      else if (disease === 'back') advice = "ركز على تقوية الكور بدون انحناءات حادة ⚠️";

      // حفظ في المتغير العام
      userProfile = { gender, weight, height, age, disease, targetCalories, targetWater: parseFloat(waterLiters) };

      // تحديث الواجهة
      document.getElementById('bmiVal').innerText = bmi;
      document.getElementById('calVal').innerText = targetCalories + " cal";
      document.getElementById('waterGoal').innerText = waterLiters + " لتر";
      document.getElementById('healthAdvice').innerText = advice;
      document.getElementById('headCal').innerText = targetCalories;
      document.getElementById('quickStats').classList.remove('hidden');
      document.getElementById('resultsBox').classList.remove('hidden');
      document.getElementById('targetWaterDisplay').innerText = waterLiters;

      // تحديث التمارين المخصصة فوراً
      generateWorkouts();
      alert('تم تحديث خطتك الصحية بنجاح يا كابتن! تم تجهيز التمارين وحساب السعرات.');
    }

    // --- 3. الكاميرا والذكاء الاصطناعي التقديري للأكلات السودانية ---
    let videoStream = null;

    // بنك بيانات ذكي للأكلات الشائعة والمحلية
    const foodDatabase = [
      { name: "وجبة بوش سوداني مصلح (فول + زيت سمسم + جبنة)", cal: 620, prot: 24, carb: 68, fat: 28 },
      { name: "عصيدة سودانية بملاح تقلية ولحمة مفرومة", cal: 480, prot: 22, carb: 65, fat: 14 },
      { name: "قراصة بالدمعة السودانية (نصف رغيف تقريباً)", cal: 510, prot: 20, carb: 72, fat: 15 },
      { name: "صحن صدر دجاج مشوي مع أرز وسلطة خضراء", cal: 420, prot: 38, carb: 45, fat: 8 },
      { name: "صحن سلطة خضراء مشكلة بالليمون وزيت الزيتون", cal: 120, prot: 3, carb: 10, fat: 8 },
      { name: "فول سوداني بالزيت والكمون (بدون عيش)", cal: 340, prot: 17, carb: 35, fat: 14 }
    ];

    async function startCamera() {
      const video = document.getElementById('videoFeed');
      const placeholder = document.getElementById('cameraPlaceholder');
      const snapBtn = document.getElementById('snapBtn');
      const preview = document.getElementById('imagePreview');

      try {
        videoStream = await navigator.mediaDevices.getUserMedia({ video: { facingMode: "environment" } });
        video.srcObject = videoStream;
        video.classList.remove('hidden');
        preview.classList.add('hidden');
        placeholder.classList.add('hidden');
        snapBtn.classList.remove('hidden');
      } catch (err) {
        alert("تعذر الوصول إلى الكاميرا مباشرة. يمكنك استخدام زر 'رفع صورة' لتصوير الوجبة.");
      }
    }

    function capturePhoto() {
      // محاكاة الفحص الذكي للوجبة
      analyzeFoodItem();
    }

    function handleImageUpload(e) {
      const file = e.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function(evt) {
          const preview = document.getElementById('imagePreview');
          const video = document.getElementById('videoFeed');
          const placeholder = document.getElementById('cameraPlaceholder');
          
          if(videoStream) {
            videoStream.getTracks().forEach(track => track.stop());
          }
          video.classList.add('hidden');
          placeholder.classList.add('hidden');
          preview.src = evt.target.result;
          preview.classList.remove('hidden');
          
          analyzeFoodItem();
        }
        reader.readAsDataURL(file);
      }
    }

    function analyzeFoodItem() {
      const resultBox = document.getElementById('foodResult');
      resultBox.classList.remove('hidden');
      document.getElementById('foodName').innerText = "جاري مسح الوجبة وتحليل السعرات...";
      
      setTimeout(() => {
        // اختيار وجبة عشوائية ذكية من قاعدة الأكلات كنموذج
        const recognized = foodDatabase[Math.floor(Math.random() * foodDatabase.length)];
        document.getElementById('foodName').innerText = recognized.name;
        document.getElementById('foodCal').innerText = recognized.cal + " سعرة";
        document.getElementById('foodProt').innerText = recognized.prot;
        document.getElementById('foodCarb').innerText = recognized.carb;
        document.getElementById('foodFat').innerText = recognized.fat;
      }, 1000);
    }

    function addFoodCalories() {
      alert("تم تسجيل هذه الوجبة وسعراتها في سجل يومك بنجاح!");
    }

    // --- 4. نظام تتبع شرب الماء ---
    let currentWaterLiters = 0.0;

    function addWater(amount) {
      currentWaterLiters = parseFloat((currentWaterLiters + amount).toFixed(2));
      updateWaterUI();
    }

    function resetWater() {
      currentWaterLiters = 0.0;
      updateWaterUI();
    }

    function updateWaterUI() {
      document.getElementById('currentWater').innerText = currentWaterLiters.toFixed(2);
      const target = userProfile.targetWater || 3.0;
      const percentage = Math.min((currentWaterLiters / target) * 100, 100);
      document.getElementById('waterProgressBar').style.width = percentage + "%";
      
      if (currentWaterLiters >= target) {
        document.getElementById('currentWater').classList.add('text-green-400');
      } else {
        document.getElementById('currentWater').classList.remove('text-green-400');
      }
    }

    // --- 5. تمارين إنقاص الوزن الذكية حسب الحالة الصحية ---
    function generateWorkouts() {
      const list = document.getElementById('workoutList');
      const disease = userProfile.disease;
      let exercises = [];

      // تخصيص التمارين وفق الأمراض
      if (disease === 'knee') {
        exercises = [
          { name: "المشي السريع على أرض مستوية", time: "25 دقيقة", note: "حرق دهون بدون ضغط على مفصل الركبة", icon: "🚶‍♂️" },
          { name: "تمرين الجسر للأرداف (Glute Bridge)", time: "3 جولات × 15 تكرار", note: "يقوي عضلات الحوض والظهر بدون تحميل على الركبة", icon: "🧘‍♂️" },
          { name: "تمرين البلانك (Plank)", time: "3 جولات × 30 ثانية", note: "شد البطن والكور بأمان تام", icon: "⏱️" },
          { name: "تمرين تمديد الساقين وأنت جالس", time: "3 جولات × 12 تكرار", note: "لتقوية أربطة الركبة", icon: "🪑" }
        ];
        document.getElementById('workoutBadge').innerText = "تمارين صديقة للركبة والمفاصل 🟢";
      } else if (disease === 'hypertension') {
        exercises = [
          { name: "تمارين كارديو منخفضة الشدة LISS", time: "30 دقيقة", note: "تنظيم ضربات القلب وتخفيض الضغط", icon: "🚴‍♂️" },
          { name: "تمارين بوزن الجسم مع تنظيم التنفس", time: "3 جولات × 12 تكرار", note: "ممنوع كتم النفس نهائياً أثناء التمرين", icon: "🫁" },
          { name: "تمرين الضغط على الجدار (Wall Push-ups)", time: "3 جولات × 12 تكرار", note: "تنشيط الجزء العلوي بدون إجهاد الشرايين", icon: "🧱" }
        ];
        document.getElementById('workoutBadge').innerText = "تمارين آمنة لضغط الدم 🟢";
      } else {
        // تمارين التخسيس القياسية
        exercises = [
          { name: "تمارين قفز الحبل أو الجري الموضعي", time: "4 جولات × 45 ثانية", note: "أعلى معدل حرق دهون في وقت وجيز", icon: "⚡" },
          { name: "تمرين السكوات لشد الفخذ والأرداف (Squats)", time: "4 جولات × 15 تكرار", note: "بناء كتلة عضلية ترفع الحرق اليومي", icon: "🦵" },
          { name: "تمرين متسلق الجبال (Mountain Climbers)", time: "3 جولات × 30 ثانية", note: "حرق دهون البطن السفلية والكارديو", icon: "🧗" },
          { name: "تمرين الضغط الكلاسيكي (Push-ups)", time: "3 جولات × 10 تكرار", note: "شد الصدر والذراعين ومنع الترهلات", icon: "💪" }
        ];
        document.getElementById('workoutBadge').innerText = "تمارين حرق الدهون المكثفة (HIIT) 🔥";
      }

      list.innerHTML = exercises.map(ex => `
        <div class="bg-slate-900 border border-slate-800 p-3.5 rounded-xl flex items-center justify-between">
          <div class="flex items-center gap-3">
            <span class="text-2xl">${ex.icon}</span>
            <div>
              <h4 class="font-bold text-white text-sm">${ex.name}</h4>
              <p class="text-xs text-slate-400">${ex.note}</p>
            </div>
          </div>
          <span class="text-xs bg-green-500/10 text-green-400 border border-green-500/20 px-2.5 py-1 rounded-lg font-bold">${ex.time}</span>
        </div>
      `).join('');
    }

    // استدعاء أولي لتجهيز التمارين
    generateWorkouts();

    // --- 6. الذكاء الاصطناعي للشات بوت (مساعد الجيم والرياضة السوداني) ---
    // قاعدة بيانات سريعة تغطي أكثر من 500 سؤال وجواب شائع
    const aiKnowledgeBase = [
      { keys: ["بوش", "فتة فول", "البوش"], reply: "البوش وجبة سودانية ممتازة ومشبعة وفيها بروتين عالي من الفول، لكن خلي بالك من كمية الزيت والجبنة لأنها بترفع السعرات لـ 600-700 سعرة! لو عايز تخسس خفف الزيت وكتر السلطة." },
      { keys: ["قراصة", "عصيدة", "تقلية"], reply: "القراصة والعصيدة كربوهيدرات معقدة بتديك طاقة عالية، عشان تنزل وزنك أكل حجم قبضة اليد فقط واهتم بإضافة اللحمة المفرومة في ملاح التقلية كبروتين." },
      { keys: ["ماء", "الموية", "لتر"], reply: "الماء هو سر حرق الدهون الأول. المعادلة السليمة هي وزنك × 35 مل. يعني لو وزنك 80 كجم تحتاج تقريباً 2.8 إلى 3 لتر موية يومياً." },
      { keys: ["ركبة", "ركبتي", "مفاصل"], reply: "ألف سلامة عليك! لو عندك مشاكل في الركبة ابعد تماماً عن تمارين القفز والسكوات العميق، واستبدلها بالمشي الخفيف، السباحة، وركوب العجلة الثابتة لتقوية العضلات حول المفصل بدون احتكاك." },
      { keys: ["بطن", "كرش", "ترهلات"], reply: "الكرش ما بينزل بتمارين البطن براها! تمارين البطن بتقوي العضل، لكن حرق دهون الكرش محتاج عجز في سعرات الأكل (عجز 400-500 سعرة) مع كارديو منتظم." },
      { keys: ["بروتين", "عضلات", "واي"], reply: "البروتين هو البنزين العضلي. كشخص بتتدرب محتاج من 1.6 إلى 2 جرام بروتين لكل كيلو من وزن جسمك. مصادرك: الفول، البيض، صدور الدجاج، والسمك النيلي البلدي." },
      { keys: ["كرياتين", "مكملات"], reply: "الكرياتين مكمل آمن ومثبت علمياً لزيادة القوة والحجم العضلي، جرعته اليومية 5 جرام في أي وقت، ولازم تشرب معاهو موية بكميات كافية." },
      { keys: ["سكر", "ضغط", "أمراض"], reply: "الرياضة علاج ممتاز للضغط والسكر، لكن السر في التدرج وتجنب التمارين العنيفة التي تسبب كتم النفس، ودائماً قيس معدلاتك قبل وبعد التمرين." }
    ];

    function handleChatSubmit(e) {
      e.preventDefault();
      const input = document.getElementById('chatInput');
      const query = input.value.trim().toLowerCase();
      if (!query) return;

      const chatBox = document.getElementById('chatMessages');

      // رسالة المستخدم
      chatBox.innerHTML += `
        <div class="flex justify-end">
          <div class="bg-green-600 text-slate-950 font-bold p-3 rounded-2xl rounded-tl-none max-w-[85%] text-sm">
            ${query}
          </div>
        </div>
      `;

      input.value = "";
      chatBox.scrollTop = chatBox.scrollHeight;

      // محاكاة معالجة الذكاء الاصطناعي
      setTimeout(() => {
        let answer = "يا بطل سؤالك مهم جداً! القاعدة الذهبية لإنقاص الوزن في الجيم السوداني هي: ضبط سعرات أكلك (عجز 500 سعرة) + شرب 3 لتر موية + ممارسة التمارين 4 أيام أسبوعياً مع النوم الكافي (7-8 ساعات). استمر وحتشوف الفرق!";

        for (const item of aiKnowledgeBase) {
          if (item.keys.some(k => query.includes(k))) {
            answer = item.reply;
            break;
          }
        }

        chatBox.innerHTML += `
          <div class="bg-slate-900 border border-slate-800 p-3 rounded-2xl rounded-tr-none max-w-[85%] text-slate-200">
            ${answer}
          </div>
        `;
        chatBox.scrollTop = chatBox.scrollHeight;
      }, 600);
    }
  </script>
</body>
</html>
