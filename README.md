<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>JOSTUM Course Registration Portal</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Supabase JS Library -->
  <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
</head>
<body class="bg-gray-100 min-h-screen text-gray-800">

  <!-- Header -->
  <header class="bg-blue-900 text-white p-4 shadow-md">
    <div class="max-w-4xl mx-auto flex justify-between items-center">
      <h1 class="text-xl font-bold">Course Registration Portal</h1>
      <button onclick="toggleAdminView()" class="bg-blue-700 hover:bg-blue-800 text-xs sm:text-sm px-3 py-1.5 rounded-lg border border-blue-400 transition">
        Admin Portal
      </button>
    </div>
  </header>

  <main class="max-w-4xl mx-auto p-4">

    <!-- STUDENT REGISTRATION FORM SECTION -->
    <div id="student-section" class="bg-white rounded-xl shadow-lg p-6 mb-8">
      <h2 class="text-2xl font-bold text-gray-800 mb-2">Student Course Registration</h2>
      <p class="text-sm text-gray-600 mb-6">Select your courses carefully. Specify if you are taking any as a carry-over course.</p>

      <div id="alert-box" class="hidden mb-4 p-3 rounded-lg text-sm"></div>

      <form id="reg-form" onsubmit="submitRegistration(event)" class="space-y-5">
        <div>
          <label class="block font-medium text-sm text-gray-700 mb-1">Full Name</label>
          <input type="text" id="fullName" required placeholder="e.g. John Doe" class="w-full border rounded-lg p-2.5 focus:ring-2 focus:ring-blue-500 outline-none">
        </div>

        <div>
          <label class="block font-medium text-sm text-gray-700 mb-1">Matriculation / Reg Number</label>
          <input type="text" id="matricNo" required placeholder="e.g. FST/2022/12345" class="w-full border rounded-lg p-2.5 focus:ring-2 focus:ring-blue-500 outline-none">
        </div>

        <div>
          <label class="block font-medium text-sm text-gray-700 mb-1">Department</label>
          <input type="text" id="department" placeholder="e.g. Computer Science" class="w-full border rounded-lg p-2.5 focus:ring-2 focus:ring-blue-500 outline-none">
        </div>

        <!-- Student Category -->
        <div>
          <label class="block font-medium text-sm text-gray-700 mb-2">Student Status</label>
          <div class="flex gap-4">
            <label class="flex items-center gap-2 cursor-pointer border p-3 rounded-lg w-full bg-gray-50 hover:bg-gray-100">
              <input type="radio" name="studentType" value="Regular" checked class="w-4 h-4 text-blue-600">
              <span class="text-sm font-medium">Regular Student</span>
            </label>
            <label class="flex items-center gap-2 cursor-pointer border p-3 rounded-lg w-full bg-gray-50 hover:bg-gray-100">
              <input type="radio" name="studentType" value="Carry Over" class="w-4 h-4 text-orange-600">
              <span class="text-sm font-medium text-orange-700">Carry Over Student</span>
            </label>
          </div>
        </div>

        <!-- Course Selection -->
        <div>
          <label class="block font-medium text-sm text-gray-700 mb-2">Select Courses Offering</label>
          <div class="grid grid-cols-2 sm:grid-cols-4 gap-3">
            <label class="flex items-center gap-2 border p-2.5 rounded-lg cursor-pointer hover:bg-blue-50">
              <input type="checkbox" value="STA 112" class="course-checkbox w-4 h-4 text-blue-600"> STA 112
            </label>
            <label class="flex items-center gap-2 border p-2.5 rounded-lg cursor-pointer hover:bg-blue-50">
              <input type="checkbox" value="CMP 112" class="course-checkbox w-4 h-4 text-blue-600"> CMP 112
            </label>
            <label class="flex items-center gap-2 border p-2.5 rounded-lg cursor-pointer hover:bg-blue-50">
              <input type="checkbox" value="CMP 122" class="course-checkbox w-4 h-4 text-blue-600"> CMP 122
            </label>
            <label class="flex items-center gap-2 border p-2.5 rounded-lg cursor-pointer hover:bg-blue-50">
              <input type="checkbox" value="PHY 102" class="course-checkbox w-4 h-4 text-blue-600"> PHY 102
            </label>
            <label class="flex items-center gap-2 border p-2.5 rounded-lg cursor-pointer hover:bg-blue-50">
              <input type="checkbox" value="PHY 108" class="course-checkbox w-4 h-4 text-blue-600"> PHY 108
            </label>
            <label class="flex items-center gap-2 border p-2.5 rounded-lg cursor-pointer hover:bg-blue-50">
              <input type="checkbox" value="GST 112" class="course-checkbox w-4 h-4 text-blue-600"> GST 112
            </label>
            <label class="flex items-center gap-2 border p-2.5 rounded-lg cursor-pointer hover:bg-blue-50">
              <input type="checkbox" value="MTH 102" class="course-checkbox w-4 h-4 text-blue-600"> MTH 102
            </label>
            <label class="flex items-center gap-2 border p-2.5 rounded-lg cursor-pointer hover:bg-blue-50">
              <input type="checkbox" value="MTH 104" class="course-checkbox w-4 h-4 text-blue-600"> MTH 104
            </label>
          </div>
        </div>

        <button type="submit" id="submit-btn" class="w-full bg-blue-900 text-white font-semibold py-3 rounded-lg hover:bg-blue-800 transition shadow">
          Submit Registration
        </button>
      </form>
    </div>

    <!-- ADMIN DASHBOARD SECTION -->
    <div id="admin-section" class="hidden bg-white rounded-xl shadow-lg p-6 mb-8">
      
      <!-- Password Lock Screen -->
      <div id="admin-lock" class="text-center py-8">
        <h3 class="text-xl font-bold mb-4">Course Representative Login</h3>
        <input type="password" id="adminPass" placeholder="Enter password" class="border p-2 rounded-lg text-center mb-4 block mx-auto w-64">
        <button onclick="loginAdmin()" class="bg-blue-900 text-white px-6 py-2 rounded-lg hover:bg-blue-800">Access Admin Portal</button>
      </div>

      <!-- Main Admin Content -->
      <div id="admin-content" class="hidden space-y-6">
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center border-b pb-4 gap-4">
          <div>
            <h2 class="text-2xl font-bold">Course Attendance & Lists</h2>
            <p class="text-sm text-gray-500">Total Registered Students Across System: <span id="total-count-badge" class="font-bold text-blue-700">0</span></p>
          </div>
          <button onclick="fetchData()" class="bg-gray-100 hover:bg-gray-200 text-sm px-3 py-1.5 rounded-lg border">
            🔄 Refresh Live Data
          </button>
        </div>

        <!-- Course Filter Tabs -->
        <div>
          <label class="block text-xs font-semibold text-gray-500 uppercase mb-2">Select Course List to View:</label>
          <div id="course-tabs" class="flex flex-wrap gap-2">
            <!-- Dynamic course tabs generated here -->
          </div>
        </div>

        <!-- Selected Course Summary Header -->
        <div class="bg-blue-50 border border-blue-200 rounded-lg p-4 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-3">
          <div>
            <h3 id="current-course-title" class="text-lg font-bold text-blue-900">STA 112 List</h3>
            <p class="text-xs text-blue-700">Total Offering Course: <span id="course-student-count" class="font-bold">0</span> students</p>
          </div>
          <button onclick="exportCourseCSV()" class="bg-green-700 hover:bg-green-800 text-white text-xs sm:text-sm px-4 py-2 rounded-lg font-medium transition shadow">
            📥 Download Course CSV
          </button>
        </div>

        <!-- Student Table -->
        <div class="overflow-x-auto border rounded-lg">
          <table class="w-full text-left text-sm">
            <thead class="bg-gray-100 border-b text-gray-700">
              <tr>
                <th class="p-3">#</th>
                <th class="p-3">Full Name</th>
                <th class="p-3">Matric No</th>
                <th class="p-3">Status</th>
                <th class="p-3">Registered Date</th>
              </tr>
            </thead>
            <tbody id="student-table-body" class="divide-y">
              <!-- Dynamically populated -->
            </tbody>
          </table>
        </div>
      </div>

    </div>

  </main>

  <script>
// Example of how your config should look:
const SUPABASE_URL = 'https://xyzcompany.supabase.co'; // Project URL
const SUPABASE_KEY = 'eyJhbGciOiJIUzI1NiIsIn...';      // Publishable / anon Key ONLY

    // ==========================================
    // 1. SUPABASE CONFIGURATION
    // Replace these two lines with your details from Supabase Project Settings -> API
    // ==========================================
    const SUPABASE_URL = 'YOUR_SUPABASE_URL';
    const SUPABASE_KEY = 'YOUR_SUPABASE_ANON_KEY';
    
    const db = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

    const COURSES = ['STA 112', 'CMP 112', 'CMP 122', 'PHY 102', 'PHY 108', 'GST 112', 'MTH 102', 'MTH 104'];
    let selectedCourseTab = 'STA 112';
    let allRegistrations = [];

    // Submit Registration
    async function submitRegistration(e) {
      e.preventDefault();
      const submitBtn = document.getElementById('submit-btn');
      const alertBox = document.getElementById('alert-box');
      
      const fullName = document.getElementById('fullName').value.trim();
      const matricNo = document.getElementById('matricNo').value.trim();
      const department = document.getElementById('department').value.trim();
      const studentType = document.querySelector('input[name="studentType"]:checked').value;
      
      const checkedCourses = Array.from(document.querySelectorAll('.course-checkbox:checked')).map(cb => cb.value);

      if (checkedCourses.length === 0) {
        showAlert('Please select at least one course!', 'bg-red-100 text-red-700');
        return;
      }

      submitBtn.disabled = true;
      submitBtn.textContent = 'Submitting...';

      const { data, error } = await db
        .from('student_registrations')
        .insert([{ 
          full_name: fullName, 
          matric_no: matricNo, 
          department: department, 
          student_type: studentType, 
          selected_courses: checkedCourses 
        }]);

      submitBtn.disabled = false;
      submitBtn.textContent = 'Submit Registration';

      if (error) {
        showAlert('Error submitting: ' + error.message, 'bg-red-100 text-red-700');
      } else {
        showAlert('🎉 Registration Successful! Details saved.', 'bg-green-100 text-green-800');
        document.getElementById('reg-form').reset();
      }
    }

    function showAlert(msg, colorClass) {
      const box = document.getElementById('alert-box');
      box.className = `mb-4 p-3 rounded-lg text-sm ${colorClass}`;
      box.textContent = msg;
      box.classList.remove('hidden');
      setTimeout(() => box.classList.add('hidden'), 5000);
    }

    function toggleAdminView() {
      const studentSec = document.getElementById('student-section');
      const adminSec = document.getElementById('admin-section');
      studentSec.classList.toggle('hidden');
      adminSec.classList.toggle('hidden');
    }

    function loginAdmin() {
      const pass = document.getElementById('adminPass').value;
      if (pass === 'course-rep') {
        document.getElementById('admin-lock').classList.add('hidden');
        document.getElementById('admin-content').classList.remove('hidden');
        renderTabs();
        fetchData();
      } else {
        alert('Incorrect Password!');
      }
    }

    // Fetch live registrations from Supabase
    async function fetchData() {
      const { data, error } = await db
        .from('student_registrations')
        .select('*')
        .order('created_at', { ascending: true });

      if (error) {
        alert('Failed to load data from Supabase: ' + error.message);
        return;
      }

      allRegistrations = data || [];
      document.getElementById('total-count-badge').textContent = allRegistrations.length;
      renderCourseList();
    }

    function renderTabs() {
      const container = document.getElementById('course-tabs');
      container.innerHTML = COURSES.map(course => `
        <button onclick="switchTab('${course}')" class="px-3 py-1.5 rounded-lg font-medium text-xs sm:text-sm border transition ${
          selectedCourseTab === course ? 'bg-blue-900 text-white border-blue-900' : 'bg-white hover:bg-gray-100 text-gray-700 border-gray-300'
        }">
          ${course}
        </button>
      `).join('');
    }

    function switchTab(course) {
      selectedCourseTab = course;
      renderTabs();
      renderCourseList();
    }

    function renderCourseList() {
      document.getElementById('current-course-title').textContent = `${selectedCourseTab} Student List`;
      
      const filtered = allRegistrations.filter(r => r.selected_courses && r.selected_courses.includes(selectedCourseTab));
      document.getElementById('course-student-count').textContent = filtered.length;

      const tbody = document.getElementById('student-table-body');
      if (filtered.length === 0) {
        tbody.innerHTML = `<tr><td colspan="5" class="p-4 text-center text-gray-400">No students registered for ${selectedCourseTab} yet.</td></tr>`;
        return;
      }

      tbody.innerHTML = filtered.map((st, idx) => `
        <tr class="hover:bg-gray-50">
          <td class="p-3 font-semibold text-gray-500">${idx + 1}</td>
          <td class="p-3 font-medium">${st.full_name}</td>
          <td class="p-3 text-gray-600">${st.matric_no}</td>
          <td class="p-3">
            <span class="px-2 py-1 rounded text-xs font-bold ${st.student_type === 'Carry Over' ? 'bg-orange-100 text-orange-700' : 'bg-green-100 text-green-700'}">
              ${st.student_type}
            </span>
          </td>
          <td class="p-3 text-xs text-gray-500">${new Date(st.created_at).toLocaleDateString()}</td>
        </tr>
      `).join('');
    }

    function exportCourseCSV() {
      const filtered = allRegistrations.filter(r => r.selected_courses && r.selected_courses.includes(selectedCourseTab));
      if (filtered.length === 0) {
        alert('No students to export for ' + selectedCourseTab);
        return;
      }

      let csvContent = "data:text/csv;charset=utf-8,S/N,Full Name,Matric Number,Department,Status,Date Registered\n";
      filtered.forEach((st, idx) => {
        csvContent += `${idx + 1},"${st.full_name}","${st.matric_no}","${st.department || ''}","${st.student_type}","${new Date(st.created_at).toLocaleDateString()}"\n`;
      });

      const encodedUri = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", encodedUri);
      link.setAttribute("download", `${selectedCourseTab}_Student_List.csv`);
      document.body.appendChild(link);
      link.click(); 
      document.body.removeChild(link);
    }
  </script>
</body>
</html>
