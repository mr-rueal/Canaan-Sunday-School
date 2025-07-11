<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Canaan Sunday School Church</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts - Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc; /* Light blue-gray background */
        }
        /* Custom CSS for smooth transitions */
        .transition-all-ease {
            transition: all 0.3s ease-in-out;
        }
        .bg-gradient-blue-green {
            background-image: linear-gradient(to right top, #2563eb, #3b82f6, #60a5fa); /* Deep blue to lighter blue */
        }
        .bg-gradient-blue-green-hover:hover {
            background-image: linear-gradient(to right top, #1d4ed8, #2563eb, #3b82f6); /* Darker on hover */
        }

        /* Modal specific styles */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7); /* Dark overlay */
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000; /* Ensure it's on top */
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease-in-out, visibility 0.3s ease-in-out;
        }
        .modal-overlay.show {
            opacity: 1;
            visibility: visible;
        }
        .modal-content {
            background-color: white;
            padding: 2.5rem; /* p-10 */
            border-radius: 1rem; /* rounded-xl */
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25); /* shadow-2xl */
            width: 90%;
            max-width: 28rem; /* max-w-md */
            text-align: center;
            position: relative;
            transform: translateY(-20px);
            opacity: 0;
            transition: transform 0.3s ease-in-out, opacity 0.3s ease-in-out;
        }
        .modal-overlay.show .modal-content {
            transform: translateY(0);
            opacity: 1;
        }

        /* Custom Alert/Message Box Styles */
        #messageBoxOverlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1001; /* Higher than login modal */
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.3s ease-in-out, visibility 0.3s ease-in-out;
        }
        #messageBoxOverlay.show {
            opacity: 1;
            visibility: visible;
        }
        #messageBoxContent {
            background-color: white;
            padding: 2rem;
            border-radius: 0.75rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            max-width: 400px;
            text-align: center;
            transform: translateY(-20px);
            opacity: 0;
            transition: transform 0.3s ease-in-out, opacity 0.3s ease-in-out;
        }
        #messageBoxOverlay.show #messageBoxContent {
            transform: translateY(0);
            opacity: 1;
        }

        /* Styles for LLM response sections */
        .llm-response-section {
            background-color: #f0f9ff; /* Light blue background */
            border-left: 4px solid #3b82f6; /* Blue left border */
            padding: 1.5rem;
            border-radius: 0.5rem;
            margin-top: 1.5rem;
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
        }
        .llm-response-section h4 {
            color: #1d4ed8; /* Darker blue heading */
            font-size: 1.25rem;
            font-weight: 600;
            margin-bottom: 0.75rem;
        }
        .llm-response-section p {
            color: #374151; /* Dark gray text */
            line-height: 1.6;
        }
        .llm-loading-indicator {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            color: #3b82f6;
            font-weight: 500;
            margin-top: 1rem;
        }
        .llm-loading-spinner {
            border: 4px solid #f3f3f3;
            border-top: 4px solid #3b82f6;
            border-radius: 50%;
            width: 24px;
            height: 24px;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
    </style>
</head>
<body>

    <!-- Header (always visible) -->
    <header class="bg-gradient-blue-green shadow-lg p-4 md:p-6 rounded-b-lg">
        <div class="container mx-auto flex flex-col md:flex-row justify-between items-center">
            <!-- Logo/Site Title -->
            <a href="#" class="text-white text-3xl font-bold mb-4 md:mb-0 rounded-md py-1 px-2 hover:opacity-90 transition-all-ease">
                Canaan Sunday School
            </a>

            <!-- Navigation -->
            <nav>
                <ul class="flex flex-wrap justify-center md:space-x-8 space-x-4">
                    <li><a href="#home" class="text-white hover:text-blue-200 text-lg font-medium transition-all-ease py-1 px-2 rounded-md">Home</a></li>
                    <li><a href="#about" class="text-white hover:text-blue-200 text-lg font-medium transition-all-ease py-1 px-2 rounded-md">Programs</a></li>
                    <li><a href="#events" class="text-white hover:text-blue-200 text-lg font-medium transition-all-ease py-1 px-2 rounded-md">Events</a></li>
                    <li><a href="#gallery" class="text-white hover:text-blue-200 text-lg font-medium transition-all-ease py-1 px-2 rounded-md">Gallery</a></li>
                    <li><a href="#team" class="text-white hover:text-blue-200 text-lg font-medium transition-all-ease py-1 px-2 rounded-md">Our Team</a></li>
                    <li><a href="#contact" class="text-white hover:text-blue-200 text-lg font-medium transition-all-ease py-1 px-2 rounded-md">Contact</a></li>
                    <!-- Login/Logout buttons in navigation -->
                    <li><button id="loginButtonNav" class="text-white hover:text-blue-200 text-lg font-medium transition-all-ease py-1 px-2 rounded-md bg-blue-700 hover:bg-blue-800">Login</button></li>
                    <li class="hidden" id="logoutNavItem"><button id="logoutBtn" class="text-white hover:text-blue-200 text-lg font-medium transition-all-ease py-1 px-2 rounded-md bg-red-600 hover:bg-red-700">Logout</button></li>
                </ul>
            </nav>
        </div>
    </header>

    <!-- Main Content (public-facing) - Initially visible -->
    <div id="mainContent">
        <main class="container mx-auto px-4 py-8">

            <!-- Hero Section -->
            <section id="home" class="bg-blue-600 text-white rounded-lg p-8 md:p-16 text-center shadow-xl mb-12">
                <h1 class="text-4xl md:text-5xl font-extrabold mb-4 leading-tight">Welcome to Canaan Sunday School</h1>
                <p class="text-lg md:text-xl mb-8 max-w-3xl mx-auto opacity-90">
                    Guiding young hearts in faith, love, and wisdom through engaging lessons and joyful fellowship.
                </p>
                <a href="#programs" class="inline-block bg-white text-blue-700 font-semibold py-3 px-8 rounded-full shadow-md hover:bg-blue-100 transform hover:scale-105 transition-all-ease">
                    Explore Our Programs
                </a>
            </section>

            <!-- About Us Section -->
            <section id="about" class="bg-white rounded-lg p-8 md:p-12 shadow-lg mb-12">
                <h2 class="text-3xl md:text-4xl font-bold text-center mb-8 text-blue-700">About Our Sunday School</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8 items-center">
                    <div>
                        <p class="text-lg leading-relaxed mb-4">
                            Canaan Sunday School is dedicated to providing a nurturing and inspiring environment for children and youth to grow in their understanding of the Bible and their relationship with God. We believe in fostering a community where every child feels loved, valued, and empowered.
                        </p>
                        <div id="moreAboutContent" class="hidden"> <!-- Use Tailwind hidden class -->
                            <p class="text-lg leading-relaxed mb-4">
                                Our curriculum is designed to be engaging and interactive, covering a wide range of biblical topics tailored to different age groups. We strive to instill core Christian values and encourage a lifelong journey of faith.
                            </p>
                            <p class="text-lg leading-relaxed">
                                Beyond lessons, we organize various activities such as community outreach programs, special holiday events, and fun learning workshops to ensure a holistic development for our students.
                            </p>
                        </div>
                        <button id="readMoreBtn" class="mt-4 inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                            Read More
                        </button>
                    </div>
                    <div class="flex justify-center">
                        <!-- Placeholder Image -->
                        <img src="https://placehold.co/400x300/e0f2fe/1d4ed8?text=Kids+Learning" alt="Kids in Sunday School" class="rounded-xl shadow-md w-full max-w-md">
                    </div>
                </div>
            </section>

            <!-- Programs Section -->
            <section id="programs" class="bg-white rounded-lg p-8 md:p-12 shadow-lg mb-12">
                <h2 class="text-3xl md:text-4xl font-bold text-center mb-8 text-blue-700">Our Programs</h2>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                    <!-- Program Card 1 -->
                    <div class="bg-blue-50 p-6 rounded-lg shadow-md hover:shadow-xl transform hover:-translate-y-2 transition-all-ease">
                        <h3 class="text-xl font-semibold mb-3 text-blue-600">Early Childhood (Ages 3-5)</h3>
                        <p class="text-gray-700 leading-relaxed">
                            Fun, interactive lessons introducing basic Bible stories and Christian values through songs, crafts, and play.
                        </p>
                    </div>
                    <!-- Program Card 2 -->
                    <div class="bg-blue-50 p-6 rounded-lg shadow-md hover:shadow-xl transform hover:-translate-y-2 transition-all-ease">
                        <h3 class="text-xl font-semibold mb-3 text-blue-600">Elementary (Ages 6-10)</h3>
                        <p class="text-gray-700 leading-relaxed">
                            Deeper dives into biblical narratives, character development, and understanding God's love through group activities.
                        </p>
                    </div>
                    <!-- Program Card 3 -->
                    <div class="bg-blue-50 p-6 rounded-lg shadow-md hover:shadow-xl transform hover:-translate-y-2 transition-all-ease">
                        <h3 class="text-xl font-semibold mb-3 text-blue-600">Youth Group (Ages 11-18)</h3>
                        <p class="text-gray-700 leading-relaxed">
                            Exploring contemporary issues through a biblical lens, fostering leadership, and building strong friendships.
                        </p>
                    </div>
                </div>
            </section>

            <!-- Events Section -->
            <section id="events" class="bg-blue-700 text-white rounded-lg p-8 md:p-12 shadow-xl mb-12">
                <h2 class="text-3xl md:text-4xl font-bold text-center mb-8">Upcoming Events</h2>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <!-- Event Card 1 -->
                    <div class="bg-white text-gray-800 p-6 rounded-lg shadow-md flex items-start space-x-4 hover:shadow-xl transform hover:scale-[1.02] transition-all-ease">
                        <div class="flex-shrink-0 bg-blue-200 text-blue-800 rounded-full h-12 w-12 flex items-center justify-center font-bold text-lg">
                            JUL<br>15
                        </div>
                        <div>
                            <h3 class="text-xl font-semibold mb-1">Summer Bible Camp</h3>
                            <p class="text-gray-600 text-sm mb-2">Monday, July 15th - Friday, July 19th</p>
                            <p class="text-gray-700">A week of exciting Bible stories, outdoor games, and creative crafts for all ages!</p>
                        </div>
                    </div>
                    <!-- Event Card 2 -->
                    <div class="bg-white text-gray-800 p-6 rounded-lg shadow-md flex items-start space-x-4 hover:shadow-xl transform hover:scale-[1.02] transition-all-ease">
                        <div class="flex-shrink-0 bg-blue-200 text-blue-800 rounded-full h-12 w-12 flex items-center justify-center font-bold text-lg">
                            AUG<br>05
                        </div>
                        <div>
                            <h3 class="text-xl font-semibold mb-1">Youth Lock-In Night</h3>
                            <p class="text-gray-600 text-sm mb-2">Friday, August 5th, 7 PM - Saturday, August 6th, 8 AM</p>
                            <p class="text-gray-700">Games, movies, fellowship, and a morning devotion for our youth group members.</p>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Gallery Section (New) -->
            <section id="gallery" class="bg-white rounded-lg p-8 md:p-12 shadow-lg mb-12 text-center">
                <h2 class="text-3xl md:text-4xl font-bold mb-8 text-blue-700">Our Gallery</h2>
                <p class="text-lg leading-relaxed mb-8 max-w-2xl mx-auto">
                    Take a look at some joyful moments from our Sunday School events, classes, and community activities!
                </p>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
                    <!-- Placeholder Images for Gallery -->
                    <div class="rounded-lg overflow-hidden shadow-md hover:shadow-xl transform hover:scale-105 transition-all-ease">
                        <img src="https://placehold.co/400x300/a7f3d0/065f46?text=Event+1" alt="Gallery Image 1" class="w-full h-48 object-cover">
                        <div class="p-4 bg-gray-50 text-gray-700 text-sm font-medium">Bible Study Fun</div>
                    </div>
                    <div class="rounded-lg overflow-hidden shadow-md hover:shadow-xl transform hover:scale-105 transition-all-ease">
                        <img src="https://placehold.co/400x300/fecaca/991b1b?text=Event+2" alt="Gallery Image 2" class="w-full h-48 object-cover">
                        <div class="p-4 bg-gray-50 text-gray-700 text-sm font-medium">Outdoor Activities</div>
                    </div>
                    <div class="rounded-lg overflow-hidden shadow-md hover:shadow-xl transform hover:scale-105 transition-all-ease">
                        <img src="https://placehold.co/400x300/bfdbfe/1e40af?text=Event+3" alt="Gallery Image 3" class="w-full h-48 object-cover">
                        <div class="p-4 bg-gray-50 text-gray-700 text-sm font-medium">Crafts and Creativity</div>
                    </div>
                    <div class="rounded-lg overflow-hidden shadow-md hover:shadow-xl transform hover:scale-105 transition-all-ease">
                        <img src="https://placehold.co/400x300/dbeafe/1c4b91?text=Event+4" alt="Gallery Image 4" class="w-full h-48 object-cover">
                        <div class="p-4 bg-gray-50 text-gray-700 text-sm font-medium">Community Outreach</div>
                    </div>
                     <div class="rounded-lg overflow-hidden shadow-md hover:shadow-xl transform hover:scale-105 transition-all-ease">
                        <img src="https://placehold.co/400x300/a7f3d0/065f46?text=Event+5" alt="Gallery Image 5" class="w-full h-48 object-cover">
                        <div class="p-4 bg-gray-50 text-gray-700 text-sm font-medium">Group Study</div>
                    </div>
                    <div class="rounded-lg overflow-hidden shadow-md hover:shadow-xl transform hover:scale-105 transition-all-ease">
                        <img src="https://placehold.co/400x300/fecaca/991b1b?text=Event+6" alt="Gallery Image 6" class="w-full h-48 object-cover">
                        <div class="p-4 bg-gray-50 text-gray-700 text-sm font-medium">Festival Celebration</div>
                    </div>
                    <div class="rounded-lg overflow-hidden shadow-md hover:shadow-xl transform hover:scale-105 transition-all-ease">
                        <img src="https://placehold.co/400x300/bfdbfe/1e40af?text=Event+7" alt="Gallery Image 7" class="w-full h-48 object-cover">
                        <div class="p-4 bg-gray-50 text-gray-700 text-sm font-medium">Story Time</div>
                    </div>
                    <div class="rounded-lg overflow-hidden shadow-md hover:shadow-xl transform hover:scale-105 transition-all-ease">
                        <img src="https://placehold.co/400x300/dbeafe/1c4b91?text=Event+8" alt="Gallery Image 8" class="w-full h-48 object-cover">
                        <div class="p-4 bg-gray-50 text-gray-700 text-sm font-medium">Team Building</div>
                    </div>
                </div>
            </section>

            <!-- New: Our Team Section -->
            <section id="team" class="bg-blue-50 rounded-lg p-8 md:p-12 shadow-lg mb-12 text-center">
                <h2 class="text-3xl md:text-4xl font-bold mb-8 text-blue-700">Our Team: Teachers and Helpers</h2>
                <p class="text-lg leading-relaxed mb-8 max-w-2xl mx-auto text-gray-700">
                    Meet the dedicated individuals who volunteer their time and talents to nurture the faith of our children and youth. Their passion makes Sunday School a joyful and enriching experience for everyone!
                </p>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8">
                    <!-- Team Member 1 -->
                    <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transform hover:-translate-y-2 transition-all-ease">
                        <img src="https://placehold.co/150x150/d1e7dd/0a3622?text=Teacher+1" alt="Teacher Name" class="rounded-full w-32 h-32 mx-auto mb-4 object-cover border-4 border-blue-200">
                        <h3 class="text-xl font-semibold text-blue-800 mb-1">Sarah Johnson</h3>
                        <p class="text-gray-600">Lead Teacher, Junior Class</p>
                    </div>
                    <!-- Team Member 2 -->
                    <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transform hover:-translate-y-2 transition-all-ease">
                        <img src="https://placehold.co/150x150/f8d7da/721c24?text=Teacher+2" alt="Teacher Name" class="rounded-full w-32 h-32 mx-auto mb-4 object-cover border-4 border-blue-200">
                        <h3 class="text-xl font-semibold text-blue-800 mb-1">Michael Lee</h3>
                        <p class="text-gray-600">Teacher, Senior Class</p>
                    </div>
                    <!-- Team Member 3 -->
                    <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transform hover:-translate-y-2 transition-all-ease">
                        <img src="https://placehold.co/150x150/d4edda/155724?text=Helper+1" alt="Helper Name" class="rounded-full w-32 h-32 mx-auto mb-4 object-cover border-4 border-blue-200">
                        <h3 class="text-xl font-semibold text-blue-800 mb-1">Emily Chen</h3>
                        <p class="text-gray-600">Assistant Helper, Sub Junior</p>
                    </div>
                    <!-- Team Member 4 -->
                    <div class="bg-white p-6 rounded-lg shadow-md hover:shadow-xl transform hover:-translate-y-2 transition-all-ease">
                        <img src="https://placehold.co/150x150/cce5ff/004085?text=Teacher+3" alt="Teacher Name" class="rounded-full w-32 h-32 mx-auto mb-4 object-cover border-4 border-blue-200">
                        <h3 class="text-xl font-semibold text-blue-800 mb-1">David Kim</h3>
                        <p class="text-gray-600">Teacher, Early Childhood</p>
                    </div>
                    <!-- Add more team members as needed -->
                </div>
            </section>


            <!-- Contact Section -->
            <section id="contact" class="bg-white rounded-lg p-8 md:p-12 shadow-lg mb-12 text-center">
                <h2 class="text-3xl md:text-4xl font-bold mb-8 text-blue-700">Get in Touch</h2>
                <p class="text-lg leading-relaxed mb-6 max-w-2xl mx-auto">
                    We'd love to hear from you! Whether you have questions about our programs, events, or simply want to learn more about our community, feel free to reach out.
                </p>
                <div class="flex flex-col md:flex-row justify-center items-center md:space-x-8 space-y-4 md:space-y-0">
                    <div class="text-center">
                        <p class="font-semibold text-xl text-blue-600">Email Us:</p>
                        <a href="mailto:info@canaansundayschool.org" class="text-blue-700 hover:underline text-lg">info@canaansundayschool.org</a>
                    </div>
                    <div class="text-center">
                        <p class="font-semibold text-xl text-blue-600">Call Us:</p>
                        <p class="text-lg">+1 (123) 456-7890</p>
                    </div>
                    <div class="text-center">
                        <p class="font-semibold text-xl text-blue-600">Visit Us:</p>
                        <p class="text-lg">123 Faith Street, Harmony City, HC 12345</p>
                    </div>
                </div>
            </section>

        </main>
    </div> <!-- End of mainContent div -->

    <!-- User Dashboard Section - Initially hidden -->
    <div id="userDashboard" class="hidden">
        <main class="container mx-auto px-4 py-8">
            <section class="bg-blue-100 rounded-lg p-8 md:p-12 shadow-lg mb-12">
                <h1 class="text-4xl md:text-5xl font-extrabold text-center mb-6 text-blue-800">
                    Welcome to Your Dashboard, <span id="dashboardUsername">User</span>!
                </h1>
                <p class="text-lg md:text-xl text-center text-gray-700 mb-8 max-w-3xl mx-auto">
                    This is your personalized space. We hope you find these memory verses inspiring.
                </p>

                <!-- Memory Verse Section (for regular user) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Memory Verses</h2>
                    <ul class="list-disc list-inside space-y-4 text-lg text-gray-800 max-w-2xl mx-auto" id="memoryVersesList">
                        <!-- Memory verses will be dynamically loaded here -->
                        <p class="text-gray-600 text-center" id="noStudentMemoryVerses">No memory verses available.</p>
                    </ul>
                    <button id="readMoreVersesBtn" class="mt-4 inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease hidden">
                        <!-- This button will only appear if there are more than 2 verses initially -->
                        Read More Verses
                    </button>
                </div>

                <!-- Your Memory Verse Recitation Status (NEW) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Your Memory Verse Recitation Status Today</h2>
                    <div id="userRecitationStatus" class="text-center text-xl font-semibold text-gray-800">
                        Loading status...
                    </div>
                </div>

                <!-- Your Attendance Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Your Attendance for Today</h2>
                    <div id="studentAttendanceStatus" class="text-center text-xl font-semibold text-gray-800">
                        Loading attendance...
                    </div>
                </div>

                <!-- Leave Application Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Submit Leave Application</h2>
                    <form id="leaveApplicationForm" class="space-y-4">
                        <div>
                            <label for="leaveStartDate" class="block text-left text-gray-700 text-sm font-bold mb-2">Start Date:</label>
                            <input type="date" id="leaveStartDate" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required>
                        </div>
                        <div>
                            <label for="leaveEndDate" class="block text-left text-gray-700 text-sm font-bold mb-2">End Date:</label>
                            <input type="date" id="leaveEndDate" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required>
                        </div>
                        <div>
                            <label for="leaveReason" class="block text-left text-gray-700 text-sm font-bold mb-2">Reason for Leave:</label>
                            <textarea id="leaveReason" rows="4" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" placeholder="e.g., Family vacation, Sickness" required></textarea>
                        </div>
                        <button type="submit" class="w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                            Submit Leave Application
                        </button>
                    </form>

                    <h3 class="text-2xl font-bold text-center mt-8 mb-4 text-blue-700">Past Applications</h3>
                    <div id="pastLeaveApplications" class="space-y-4">
                        <!-- Past leave applications will be dynamically loaded here -->
                        <p class="text-gray-600 text-center" id="noPastApplications">No past leave applications found.</p>
                    </div>
                </div>

                <!-- New: Notice Board Section (Student View) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Notice Board</h2>
                    <div id="studentNoticesDisplay" class="space-y-4">
                        <p class="text-gray-600 text-center" id="noStudentNotices">No notices available.</p>
                        <!-- Notices will be dynamically loaded here -->
                    </div>
                </div>

                <!-- New: Downloads Centre Section (Student View) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Downloads Centre</h2>
                    <div id="downloadsCentreContent" class="space-y-4">
                        <p class="text-gray-700 text-center mb-4">
                            Access important documents, worksheets, and resources here.
                        </p>
                        <ul class="list-disc list-inside space-y-2 text-lg text-gray-800 max-w-2xl mx-auto" id="userDownloadsList">
                            <!-- Downloadable items will be dynamically loaded here -->
                            <p class="text-gray-600 text-center" id="noUserDownloads">No downloadable resources available.</p>
                        </ul>
                    </div>
                </div>

            </section>
        </main>
    </div> <!-- End of userDashboard div -->


    <!-- Admin Dashboard Section - Initially hidden -->
    <div id="adminDashboard" class="hidden">
        <main class="container mx-auto px-4 py-8">
            <section class="bg-purple-100 rounded-lg p-8 md:p-12 shadow-lg mb-12">
                <h1 class="text-4xl md:text-5xl font-extrabold text-center mb-6 text-purple-800">
                    Admin Dashboard
                </h1>
                <p class="text-lg md:text-xl text-center text-gray-700 mb-8 max-w-3xl mx-auto">
                    Manage student information and attendance for all Sunday School sections.
                </p>

                <!-- Total Present Students Today (Updated from Total Enrolled) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Total Present Students Today</h2>
                    <div id="totalStudentsCount" class="text-center text-5xl font-extrabold text-blue-600 py-4">
                        0
                    </div>
                    <p class="text-center text-gray-600">Number of students marked as present for today's class.</p>
                </div>

                <!-- New: Attendance Submission Review (Admin View) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Attendance Submission Review</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Review and manage submitted attendance records from teachers.
                    </p>
                    <div id="attendanceNotificationsList" class="space-y-4">
                        <p class="text-gray-600 text-center" id="noAttendanceNotifications">No pending attendance notifications.</p>
                        <!-- Attendance notifications will be dynamically loaded here -->
                    </div>
                </div>

                <!-- Admin Sub Junior Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Sub Junior (Ages 3-5) Management</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Manage Sub Junior student details and record their attendance.
                    </p>

                    <p class="text-center mt-4">
                        <button id="adminViewSubJuniorStudentsBtn" class="inline-block bg-green-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-green-600 transition-all-ease">
                            View Sub Junior Students
                        </button>
                    </p>

                    <div id="adminSubJuniorStudentsTableContainer" class="overflow-x-auto hidden mt-6">
                        <h3 class="text-2xl font-semibold text-center mb-4 text-blue-600">Enrolled Students</h3>
                        <table class="min-w-full bg-white border border-gray-300 rounded-lg shadow-sm">
                            <thead>
                                <tr class="bg-blue-50 border-b border-gray-300">
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Name</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Age</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Mother Name</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Father Name</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider rounded-tr-lg">Phone Number</th>
                                </tr>
                            </thead>
                            <tbody id="subJuniorStudentsTableBody">
                                <!-- Sub Junior student data will be dynamically populated -->
                            </tbody>
                        </table>
                    </div>

                    <!-- Admin Sub Junior Attendance Form -->
                    <p class="text-center mt-6">
                        <button id="adminMarkSubJuniorAttendanceBtn" class="inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                            Mark Sub Junior Attendance
                        </button>
                    </p>
                    <div id="adminSubJuniorAttendanceFormContainer" class="hidden bg-gray-50 p-6 rounded-lg mt-6 shadow-sm">
                        <h3 class="text-2xl font-semibold text-center mb-4 text-blue-600">Mark Today's Attendance</h3>
                        <div class="flex justify-center space-x-4 mb-4">
                            <button type="button" class="mark-all-present-btn bg-blue-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-600 transition-all-ease" data-grade="subJunior">Mark All Present</button>
                            <button type="button" class="mark-all-absent-btn bg-red-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-red-600 transition-all-ease" data-grade="subJunior">Mark All Absent</button>
                        </div>
                        <form id="adminSubJuniorAttendanceForm" class="space-y-3">
                            <div id="subJuniorAttendanceCheckboxes" class="grid grid-cols-2 gap-4 text-left">
                                <!-- Sub Junior attendance checkboxes will be dynamically populated -->
                            </div>
                            <button type="submit" class="mt-6 w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                                Submit Attendance
                            </button>
                        </form>
                    </div>
                </div>

                <!-- Admin Junior Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Junior (Ages 6-10) Management</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Manage Junior student details and record their attendance.
                    </p>
                    <p class="text-center mt-4">
                        <button id="adminViewJuniorStudentsBtn" class="inline-block bg-green-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-green-600 transition-all-ease">
                            View Junior Students
                        </button>
                    </p>
                    <div id="adminJuniorStudentsTableContainer" class="overflow-x-auto hidden mt-6">
                        <h3 class="text-2xl font-semibold text-center mb-4 text-blue-600">Enrolled Students</h3>
                        <table class="min-w-full bg-white border border-gray-300 rounded-lg shadow-sm">
                            <thead>
                                <tr class="bg-blue-50 border-b border-gray-300">
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Name</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Age</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Mother Name</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Father Name</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider rounded-tr-lg">Phone Number</th>
                                </tr>
                            </thead>
                            <tbody id="juniorStudentsTableBody">
                                <!-- Junior student data will be dynamically populated -->
                            </tbody>
                        </table>
                    </div>

                    <!-- Admin Junior Attendance Form -->
                    <p class="text-center mt-6">
                        <button id="adminMarkJuniorAttendanceBtn" class="inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                            Mark Junior Attendance
                        </button>
                    </p>
                    <div id="adminJuniorAttendanceFormContainer" class="hidden bg-gray-50 p-6 rounded-lg mt-6 shadow-sm">
                        <h3 class="text-2xl font-semibold text-center mb-4 text-blue-600">Mark Today's Attendance</h3>
                        <div class="flex justify-center space-x-4 mb-4">
                            <button type="button" class="mark-all-present-btn bg-blue-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-600 transition-all-ease" data-grade="junior">Mark All Present</button>
                            <button type="button" class="mark-all-absent-btn bg-red-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-red-600 transition-all-ease" data-grade="junior">Mark All Absent</button>
                        </div>
                        <form id="adminJuniorAttendanceForm" class="space-y-3">
                            <div id="juniorAttendanceCheckboxes" class="grid grid-cols-2 gap-4 text-left">
                                <!-- Junior attendance checkboxes will be dynamically populated -->
                            </div>
                            <button type="submit" class="mt-6 w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                                Submit Attendance
                            </button>
                        </form>
                    </div>
                </div>

                <!-- Admin Senior Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Senior (Ages 11-18) Management</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Manage Senior youth group member details and record their attendance.
                    </p>
                    <p class="text-center mt-4">
                        <button id="adminViewSeniorStudentsBtn" class="inline-block bg-green-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-green-600 transition-all-ease">
                            View Senior Students
                        </button>
                    </p>
                    <div id="adminSeniorStudentsTableContainer" class="overflow-x-auto hidden mt-6">
                        <h3 class="text-2xl font-semibold text-center mb-4 text-blue-600">Enrolled Students</h3>
                        <table class="min-w-full bg-white border border-gray-300 rounded-lg shadow-sm">
                            <thead>
                                <tr class="bg-blue-50 border-b border-gray-300">
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Name</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Age</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Mother Name</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider">Father Name</th>
                                    <th class="py-3 px-4 text-left text-sm font-semibold text-blue-700 uppercase tracking-wider rounded-tr-lg">Phone Number</th>
                                </tr>
                            </thead>
                            <tbody id="seniorStudentsTableBody">
                                <!-- Senior student data will be dynamically populated -->
                            </tbody>
                        </table>
                    </div>

                    <!-- Admin Senior Attendance Form -->
                    <p class="text-center mt-6">
                        <button id="adminMarkSeniorAttendanceBtn" class="inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                            Mark Senior Attendance
                        </button>
                    </p>
                    <div id="adminSeniorAttendanceFormContainer" class="hidden bg-gray-50 p-6 rounded-lg mt-6 shadow-sm">
                        <h3 class="text-2xl font-semibold text-center mb-4 text-blue-600">Mark Today's Attendance</h3>
                        <div class="flex justify-center space-x-4 mb-4">
                            <button type="button" class="mark-all-present-btn bg-blue-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-600 transition-all-ease" data-grade="senior">Mark All Present</button>
                            <button type="button" class="mark-all-absent-btn bg-red-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-red-600 transition-all-ease" data-grade="senior">Mark All Absent</button>
                        </div>
                        <form id="adminSeniorAttendanceForm" class="space-y-3">
                            <div id="seniorAttendanceCheckboxes" class="grid grid-cols-2 gap-4 text-left">
                                <!-- Senior attendance checkboxes will be dynamically populated -->
                            </div>
                            <button type="submit" class="mt-6 w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                                Submit Attendance
                            </button>
                        </form>
                    </div>
                </div>

                <!-- Leave Applications Management Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Leave Applications Management</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Review and manage pending leave applications from students.
                    </p>
                    <div id="pendingLeaveApplications" class="space-y-4">
                        <p class="text-gray-600 text-center" id="noPendingApplications">No pending leave applications.</p>
                        <!-- Pending leave applications will be loaded here -->
                    </div>
                </div>

                <!-- New: Notice Board Management Section (Admin View) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Notice Board Management</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Add, edit, or delete notices for the student dashboard.
                    </p>

                    <form id="noticeForm" class="space-y-4 mb-8">
                        <input type="hidden" id="noticeId" value=""> <!-- Hidden field for notice ID when editing -->
                        <div>
                            <label for="noticeTitle" class="block text-left text-gray-700 text-sm font-bold mb-2">Notice Title:</label>
                            <input type="text" id="noticeTitle" placeholder="Enter notice title" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required>
                        </div>
                        <div>
                            <label for="noticeContent" class="block text-left text-gray-700 text-sm font-bold mb-2">Notice Content:</label>
                            <textarea id="noticeContent" rows="4" placeholder="Enter notice content" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required></textarea>
                        </div>
                        <button type="submit" id="submitNoticeBtn" class="w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                            Add New Notice
                        </button>
                        <button type="button" id="cancelEditNoticeBtn" class="w-full bg-gray-400 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-gray-500 transition-all-ease hidden mt-2">
                            Cancel Edit
                        </button>
                    </form>

                    <h3 class="text-2xl font-bold text-center mt-8 mb-4 text-blue-700">Current Notices</h3>
                    <div id="adminNoticesList" class="space-y-4">
                        <p class="text-gray-600 text-center" id="noAdminNotices">No notices currently posted.</p>
                        <!-- Existing notices will be dynamically loaded here -->
                    </div>
                </div>

                <!-- New: Memory Verse Management (Admin View) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Memory Verse Management</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Add, edit, or delete memory verses for students.
                    </p>
                    <form id="memoryVerseForm" class="space-y-4 mb-8">
                        <input type="hidden" id="memoryVerseId" value="">
                        <div>
                            <label for="memoryVerseText" class="block text-left text-gray-700 text-sm font-bold mb-2">Verse Text:</label>
                            <textarea id="memoryVerseText" rows="3" placeholder="e.g., For God so loved the world..." class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required></textarea>
                        </div>
                        <div>
                            <label for="memoryVerseReference" class="block text-left text-gray-700 text-sm font-bold mb-2">Verse Reference:</label>
                            <input type="text" id="memoryVerseReference" placeholder="e.g., John 3:16 (ESV)" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required>
                        </div>
                        <button type="submit" id="submitMemoryVerseBtn" class="w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                            Add New Verse
                        </button>
                        <button type="button" id="cancelEditMemoryVerseBtn" class="w-full bg-gray-400 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-gray-500 transition-all-ease hidden mt-2">
                            Cancel Edit
                        </button>
                    </form>
                    <h3 class="text-2xl font-bold text-center mt-8 mb-4 text-blue-700">Current Memory Verses</h3>
                    <div id="adminMemoryVersesList" class="space-y-4">
                        <p class="text-gray-600 text-center" id="noAdminMemoryVerses">No memory verses currently posted.</p>
                        <!-- Existing memory verses will be dynamically loaded here -->
                    </div>
                </div>

                <!-- NEW: Memory Verse Recitation Tracking (Admin View) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Memory Verse Recitation Tracking</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Mark which students have recited their memory verses for a specific date.
                    </p>

                    <div class="mb-6">
                        <label for="recitationDateInput" class="block text-left text-gray-700 text-sm font-bold mb-2">Select Date:</label>
                        <input type="date" id="recitationDateInput" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" value="">
                    </div>

                    <!-- Sub Junior Recitation -->
                    <div class="mb-8">
                        <h3 class="text-2xl font-bold text-center mb-4 text-blue-600">Sub Junior Recitation</h3>
                        <p class="text-center mt-4">
                            <button id="adminViewSubJuniorRecitationBtn" class="inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                                View Sub Junior Recitation
                            </button>
                        </p>
                        <div id="adminSubJuniorRecitationContainer" class="hidden bg-gray-50 p-6 rounded-lg mt-6 shadow-sm">
                            <form id="adminSubJuniorRecitationForm" class="space-y-3">
                                <div id="subJuniorRecitationCheckboxes" class="grid grid-cols-2 gap-4 text-left">
                                    <!-- Sub Junior recitation checkboxes will be dynamically populated -->
                                </div>
                                <button type="submit" class="mt-6 w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                                    Submit Sub Junior Recitation Marks
                                </button>
                            </form>
                        </div>
                    </div>

                    <!-- Junior Recitation -->
                    <div class="mb-8">
                        <h3 class="text-2xl font-bold text-center mb-4 text-blue-600">Junior Recitation</h3>
                        <p class="text-center mt-4">
                            <button id="adminViewJuniorRecitationBtn" class="inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                                View Junior Recitation
                            </button>
                        </p>
                        <div id="adminJuniorRecitationContainer" class="hidden bg-gray-50 p-6 rounded-lg mt-6 shadow-sm">
                            <form id="adminJuniorRecitationForm" class="space-y-3">
                                <div id="juniorRecitationCheckboxes" class="grid grid-cols-2 gap-4 text-left">
                                    <!-- Junior recitation checkboxes will be dynamically populated -->
                                </div>
                                <button type="submit" class="mt-6 w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                                    Submit Junior Recitation Marks
                                </button>
                            </form>
                        </div>
                    </div>

                    <!-- Senior Recitation -->
                    <div class="mb-8">
                        <h3 class="text-2xl font-bold text-center mb-4 text-blue-600">Senior Recitation</h3>
                        <p class="text-center mt-4">
                            <button id="adminViewSeniorRecitationBtn" class="inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                                View Senior Recitation
                            </button>
                        </p>
                        <div id="adminSeniorRecitationContainer" class="hidden bg-gray-50 p-6 rounded-lg mt-6 shadow-sm">
                            <form id="adminSeniorRecitationForm" class="space-y-3">
                                <div id="seniorRecitationCheckboxes" class="grid grid-cols-2 gap-4 text-left">
                                    <!-- Senior recitation checkboxes will be dynamically populated -->
                                </div>
                                <button type="submit" class="mt-6 w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                                    Submit Senior Recitation Marks
                                </button>
                            </form>
                        </div>
                    </div>
                </div>


                <!-- New: Lesson Plan Idea Generator (Admin View) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">✨ Lesson Plan Idea Generator</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Enter a topic below to get creative lesson ideas, discussion questions, and activity suggestions.
                    </p>
                    <form id="lessonIdeaForm" class="space-y-4">
                        <div>
                            <label for="lessonTopic" class="block text-left text-gray-700 text-sm font-bold mb-2">Lesson Topic:</label>
                            <input type="text" id="lessonTopic" placeholder="e.g., The Parable of the Good Samaritan, Forgiveness" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required>
                        </div>
                        <button type="submit" id="generateLessonIdeasBtn" class="w-full bg-purple-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-purple-700 transition-all-ease">
                            ✨ Generate Ideas
                        </button>
                    </form>
                    <div id="lessonIdeasOutput" class="llm-response-section hidden">
                        <h4 class="text-xl font-semibold mb-3">Generated Lesson Ideas:</h4>
                        <div id="lessonIdeasContent"></div>
                    </div>
                    <div id="lessonIdeasLoading" class="llm-loading-indicator hidden">
                        <div class="llm-loading-spinner"></div>
                        <span>Generating ideas...</span>
                    </div>
                </div>

                <!-- New: Downloads Centre Management (Admin View) -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Downloads Centre Management</h2>
                    <p class="text-lg text-gray-800 leading-relaxed max-w-2xl mx-auto mb-6">
                        Add, edit, or delete downloadable resources for students and teachers.
                    </p>

                    <form id="downloadForm" class="space-y-4 mb-8">
                        <input type="hidden" id="downloadId" value="">
                        <div>
                            <label for="downloadTitle" class="block text-left text-gray-700 text-sm font-bold mb-2">Title:</label>
                            <input type="text" id="downloadTitle" placeholder="e.g., Sunday School Handbook" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required>
                        </div>
                        <div>
                            <label for="downloadDescription" class="block text-left text-gray-700 text-sm font-bold mb-2">Description (Optional):</label>
                            <textarea id="downloadDescription" rows="2" placeholder="Brief description of the file" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"></textarea>
                        </div>
                        <div>
                            <label for="downloadUrl" class="block text-left text-gray-700 text-sm font-bold mb-2">File URL:</label>
                            <input type="url" id="downloadUrl" placeholder="e.g., https://example.com/handbook.pdf" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" required>
                        </div>
                        <div>
                            <label for="downloadCategory" class="block text-left text-gray-700 text-sm font-bold mb-2">Category (e.g., All, Junior, Teacher):</label>
                            <input type="text" id="downloadCategory" placeholder="e.g., All Grades, Junior Class" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                        </div>
                        <button type="submit" id="submitDownloadBtn" class="w-full bg-blue-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-700 transition-all-ease">
                            Add New Download
                        </button>
                        <button type="button" id="cancelEditDownloadBtn" class="w-full bg-gray-400 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-gray-500 transition-all-ease hidden mt-2">
                            Cancel Edit
                        </button>
                    </form>

                    <h3 class="text-2xl font-bold text-center mt-8 mb-4 text-blue-700">Current Downloads</h3>
                    <div id="adminDownloadsList" class="space-y-4">
                        <p class="text-gray-600 text-center" id="noAdminDownloads">No downloadable files currently posted.</p>
                        <!-- Existing downloads will be dynamically loaded here -->
                    </div>
                </div>


            </section>
        </main>
    </div> <!-- End of adminDashboard div -->

    <!-- Teacher Dashboard Section - Newly added -->
    <div id="teacherDashboard" class="hidden">
        <main class="container mx-auto px-4 py-8">
            <section class="bg-green-100 rounded-lg p-8 md:p-12 shadow-lg mb-12">
                <h1 class="text-4xl md:text-5xl font-extrabold text-center mb-6 text-green-800">
                    Teacher Dashboard
                </h1>
                <p class="text-lg md:text-xl text-center text-gray-700 mb-8 max-w-3xl mx-auto">
                    Manage your classes, mark attendance, and review student applications.
                </p>

                <!-- Teacher Sub Junior Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-green-700">Sub Junior (Ages 3-5) Class</h2>
                    <p class="text-center mt-4">
                        <button id="teacherViewSubJuniorStudentsBtn" class="inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                            View Students & Mark Attendance
                        </button>
                    </p>
                    <div id="teacherSubJuniorClassDetails" class="hidden mt-6">
                        <h3 class="text-2xl font-semibold text-center mb-4 text-green-600">Students & Today's Attendance</h3>
                        <form id="teacherSubJuniorAttendanceForm" class="space-y-3">
                            <div class="flex justify-center space-x-4 mb-4">
                                <button type="button" class="mark-all-present-btn bg-blue-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-600 transition-all-ease" data-grade="subJunior">Mark All Present</button>
                                <button type="button" class="mark-all-absent-btn bg-red-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-red-600 transition-all-ease" data-grade="subJunior">Mark All Absent</button>
                            </div>
                            <table class="min-w-full bg-white border border-gray-300 rounded-lg shadow-sm mb-4">
                                <thead>
                                    <tr class="bg-green-50 border-b border-gray-300">
                                        <th class="py-3 px-4 text-left text-sm font-semibold text-green-700 uppercase tracking-wider">Name</th>
                                        <th class="py-3 px-4 text-left text-sm font-semibold text-green-700 uppercase tracking-wider">Age</th>
                                        <th class="py-3 px-4 text-left text-sm font-semibold text-green-700 uppercase tracking-wider rounded-tr-lg">Present</th>
                                    </tr>
                                </thead>
                                <tbody id="teacherSubJuniorStudentsTableBody">
                                    <!-- Sub Junior student data and attendance checkboxes -->
                                </tbody>
                            </table>
                            <button type="submit" class="w-full bg-green-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-green-700 transition-all-ease">
                                Submit Attendance
                            </button>
                        </form>
                    </div>
                </div>

                <!-- Teacher Junior Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-green-700">Junior (Ages 6-10) Class</h2>
                    <p class="text-center mt-4">
                        <button id="teacherViewJuniorStudentsBtn" class="inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                            View Students & Mark Attendance
                        </button>
                    </p>
                    <div id="teacherJuniorClassDetails" class="hidden mt-6">
                        <h3 class="text-2xl font-semibold text-center mb-4 text-green-600">Students & Today's Attendance</h3>
                        <form id="teacherJuniorAttendanceForm" class="space-y-3">
                            <div class="flex justify-center space-x-4 mb-4">
                                <button type="button" class="mark-all-present-btn bg-blue-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-600 transition-all-ease" data-grade="junior">Mark All Present</button>
                                <button type="button" class="mark-all-absent-btn bg-red-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-red-600 transition-all-ease" data-grade="junior">Mark All Absent</button>
                            </div>
                            <table class="min-w-full bg-white border border-gray-300 rounded-lg shadow-sm mb-4">
                                <thead>
                                    <tr class="bg-green-50 border-b border-gray-300">
                                        <th class="py-3 px-4 text-left text-sm font-semibold text-green-700 uppercase tracking-wider">Name</th>
                                        <th class="py-3 px-4 text-left text-sm font-semibold text-green-700 uppercase tracking-wider">Age</th>
                                        <th class="py-3 px-4 text-left text-sm font-semibold text-green-700 uppercase tracking-wider rounded-tr-lg">Present</th>
                                    </tr>
                                </thead>
                                <tbody id="teacherJuniorStudentsTableBody">
                                    <!-- Junior student data and attendance checkboxes -->
                                </tbody>
                            </table>
                            <button type="submit" class="w-full bg-green-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-green-700 transition-all-ease">
                                Submit Attendance
                            </button>
                        </form>
                    </div>
                </div>

                <!-- Teacher Senior Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-green-700">Senior (Ages 11-18) Class</h2>
                    <p class="text-center mt-4">
                        <button id="teacherViewSeniorStudentsBtn" class="inline-block bg-blue-500 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-blue-600 transition-all-ease">
                            View Students & Mark Attendance
                        </button>
                    </p>
                    <div id="teacherSeniorClassDetails" class="hidden mt-6">
                        <h3 class="text-2xl font-semibold text-center mb-4 text-green-600">Students & Today's Attendance</h3>
                        <form id="teacherSeniorAttendanceForm" class="space-y-3">
                            <div class="flex justify-center space-x-4 mb-4">
                                <button type="button" class="mark-all-present-btn bg-blue-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-blue-600 transition-all-ease" data-grade="senior">Mark All Present</button>
                                <button type="button" class="mark-all-absent-btn bg-red-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-red-600 transition-all-ease" data-grade="senior">Mark All Absent</button>
                            </div>
                            <table class="min-w-full bg-white border border-gray-300 rounded-lg shadow-sm mb-4">
                                <thead>
                                    <tr class="bg-green-50 border-b border-gray-300">
                                        <th class="py-3 px-4 text-left text-sm font-semibold text-green-700 uppercase tracking-wider">Name</th>
                                        <th class="py-3 px-4 text-left text-sm font-semibold text-green-700 uppercase tracking-wider">Age</th>
                                        <th class="py-3 px-4 text-left text-sm font-semibold text-green-700 uppercase tracking-wider rounded-tr-lg">Present</th>
                                    </tr>
                                </thead>
                                <tbody id="teacherSeniorStudentsTableBody">
                                    <!-- Senior student data and attendance checkboxes -->
                                </tbody>
                            </table>
                            <button type="submit" class="w-full bg-green-600 text-white font-semibold py-2 px-6 rounded-full shadow-md hover:bg-green-700 transition-all-ease">
                                Submit Attendance
                            </button>
                        </form>
                    </div>
                </div>

                <!-- Teacher View Notices Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Notices for Teachers</h2>
                    <div id="teacherNoticesDisplay" class="space-y-4">
                        <p class="text-gray-600 text-center" id="noTeacherNotices">No notices available.</p>
                        <!-- Notices will be dynamically loaded here (same as student view) -->
                    </div>
                </div>

                <!-- Teacher View Leave Applications Section -->
                <div class="bg-white p-6 rounded-lg shadow-md mt-8">
                    <h2 class="text-3xl font-bold text-center mb-6 text-blue-700">Student Leave Applications</h2>
                    <div id="teacherPendingLeaveApplications" class="space-y-4">
                        <p class="text-gray-600 text-center" id="noTeacherPendingApplications">No pending leave applications.</p>
                        <!-- Pending leave applications for teachers to view/approve/disapprove -->
                    </div>
                </div>

            </section>
        </main>
    </div> <!-- End of teacherDashboard div -->


    <!-- Footer (always visible) -->
    <footer class="bg-gray-800 text-white p-6 rounded-t-lg text-center shadow-inner">
        <div class="container mx-auto">
            <p>&copy; 2025 Canaan Sunday School Church. All rights reserved.</p>
            <p class="text-sm mt-2">
                <a href="#" class="text-blue-300 hover:text-blue-100 transition-all-ease">Privacy Policy</a> |
                <a href="#" class="text-blue-300 hover:text-blue-100 transition-all-ease">Terms of Service</a>
            </p>
        </div>
    </footer>

    <!-- Login Modal -->
    <div id="loginModal" class="modal-overlay">
        <div class="modal-content">
            <button id="closeModalBtn" class="absolute top-4 right-4 text-gray-500 hover:text-gray-700 text-3xl font-bold leading-none">&times;</button>
            <h2 id="modalTitle" class="text-3xl font-bold text-blue-700 mb-6">Canaan Sunday School Login</h2>
            <p class="text-gray-600 mb-6">Enter your credentials to access site features.</p>
            <form id="loginForm" class="space-y-5">
                <div>
                    <input type="text" id="username" placeholder="Username" class="w-full px-4 py-3 rounded-lg border-2 border-gray-300 focus:outline-none focus:border-blue-500 transition-all-ease" required>
                </div>
                <div>
                    <input type="password" id="password" placeholder="Password" class="w-full px-4 py-3 rounded-lg border-2 border-gray-300 focus:outline-none focus:border-blue-500 transition-all-ease" required>
                </div>
                <p id="loginMessage" class="text-red-600 text-sm hidden">Invalid username or password.</p>
                <button type="submit" class="w-full bg-blue-600 text-white font-semibold py-3 rounded-lg shadow-md hover:bg-blue-700 transform hover:scale-105 transition-all-ease">
                    Login
                </button>
            </form>
        </div>
    </div>

    <!-- Custom Message Box for alerts -->
    <div id="messageBoxOverlay" class="modal-overlay">
        <div id="messageBoxContent" class="modal-content">
            <h3 id="messageBoxTitle" class="text-2xl font-bold mb-4">Message</h3>
            <p id="messageBoxText" class="text-lg mb-6"></p>
            <button id="messageBoxCloseBtn" class="bg-blue-600 text-white font-semibold py-2 px-6 rounded-lg shadow-md hover:bg-blue-700 transition-all-ease">
                OK
            </button>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, getDoc, collection, query, where, updateDoc, deleteDoc, getDocs, serverTimestamp, onSnapshot, addDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Firebase Initialization (global scope for access)
        let app, db, auth;
        let currentUserId = null; // To store the authenticated user's ID
        let currentUsername = null; // To store the logged-in username

        // These variables are provided by the Canvas environment at runtime
        // Access them via window object as they are global
        const appId = typeof window.__app_id !== 'undefined' ? window.__app_id : 'default-app-id';
        const firebaseConfig = typeof window.__firebase_config !== 'undefined' ? JSON.parse(window.__firebase_config) : {};

        // Custom message box functions
        function showMessageBox(title, message) {
            const messageBoxOverlay = document.getElementById('messageBoxOverlay');
            const messageBoxTitle = document.getElementById('messageBoxTitle');
            const messageBoxText = document.getElementById('messageBoxText');
            const messageBoxCloseBtn = document.getElementById('messageBoxCloseBtn');

            messageBoxTitle.textContent = title;
            messageBoxText.textContent = message;
            messageBoxOverlay.classList.add('show');

            const closeHandler = () => {
                messageBoxOverlay.classList.remove('show');
                messageBoxCloseBtn.removeEventListener('click', closeHandler);
            };
            messageBoxCloseBtn.addEventListener('click', closeHandler);
            messageBoxOverlay.addEventListener('click', (event) => {
                if (event.target === messageBoxOverlay) {
                    closeHandler();
                }
            });
        }

        document.addEventListener('DOMContentLoaded', function() {
            // Initialize Firebase when DOM is ready
            app = initializeApp(firebaseConfig);
            db = getFirestore(app);
            auth = getAuth(app);

            onAuthStateChanged(auth, async (user) => {
                if (!user) {
                    try {
                        // Use __initial_auth_token if available (Canvas environment)
                        // Otherwise, sign in anonymously for local development/testing
                        if (typeof window.__initial_auth_token !== 'undefined') {
                            await signInWithCustomToken(auth, window.__initial_auth_token);
                            console.log("Firebase: Signed in with custom token.");
                        } else {
                            await signInAnonymously(auth);
                            console.log("Firebase: Signed in anonymously.");
                        }
                    } catch (error) {
                        console.error("Firebase Auth Error:", error);
                        showMessageBox("Authentication Error", "Could not sign in to Firebase. Some features may not work.");
                    }
                }
                // Ensure currentUserId is set after any auth attempt
                currentUserId = auth.currentUser?.uid || crypto.randomUUID();
                console.log("Firebase: Current User ID:", currentUserId);
            });


            // Read More/Less functionality for About Us section
            const readMoreAboutBtn = document.getElementById('readMoreBtn');
            const moreAboutContent = document.getElementById('moreAboutContent');

            if (readMoreAboutBtn && moreAboutContent) {
                readMoreAboutBtn.addEventListener('click', function() {
                    moreAboutContent.classList.toggle('hidden');
                    if (moreAboutContent.classList.contains('hidden')) {
                        readMoreAboutBtn.textContent = 'Read More';
                    } else {
                        readMoreAboutBtn.textContent = 'Read Less';
                    }
                });
            }

            // Login Modal Elements
            const loginModal = document.getElementById('loginModal');
            const modalTitle = document.getElementById('modalTitle');
            const closeModalBtn = document.getElementById('closeModalBtn');
            const loginForm = document.getElementById('loginForm');
            const usernameInput = loginModal.querySelector('#username');
            const passwordInput = loginModal.querySelector('#password');
            const loginMessage = loginModal.querySelector('#loginMessage');

            // Header Navigation Buttons
            const loginButtonNav = document.getElementById('loginButtonNav');
            const logoutBtn = document.getElementById('logoutBtn');
            const logoutNavItem = document.getElementById('logoutNavItem');

            // Content Sections
            const mainContent = document.getElementById('mainContent');
            const userDashboard = document.getElementById('userDashboard');
            const adminDashboard = document.getElementById('adminDashboard');
            const teacherDashboard = document.getElementById('teacherDashboard'); // New: Teacher Dashboard
            const dashboardUsernameSpan = document.getElementById('dashboardUsername');
            const studentAttendanceStatusDiv = document.getElementById('studentAttendanceStatus');
            const userRecitationStatusDiv = document.getElementById('userRecitationStatus'); // NEW

            // Leave Application Elements (Student Dashboard)
            const leaveApplicationForm = document.getElementById('leaveApplicationForm');
            const leaveStartDateInput = document.getElementById('leaveStartDate');
            const leaveEndDateInput = document.getElementById('leaveEndDate');
            const leaveReasonInput = document.getElementById('leaveReason');
            const pastLeaveApplicationsDiv = document.getElementById('pastLeaveApplications');
            const noPastApplicationsMsg = document.getElementById('noPastApplications');

            // Leave Application Elements (Admin Dashboard)
            const pendingLeaveApplicationsDiv = document.getElementById('pendingLeaveApplications');
            const noPendingApplicationsMsg = document.getElementById('noPendingApplications');

            // Notice Board Elements (Student)
            const studentNoticesDisplay = document.getElementById('studentNoticesDisplay');
            const noStudentNoticesMsg = document.getElementById('noStudentNotices');

            // Notice Board Elements (Admin)
            const noticeForm = document.getElementById('noticeForm');
            const noticeIdInput = document.getElementById('noticeId');
            const noticeTitleInput = document.getElementById('noticeTitle');
            const noticeContentInput = document.getElementById('noticeContent');
            const submitNoticeBtn = document.getElementById('submitNoticeBtn');
            const cancelEditNoticeBtn = document.getElementById('cancelEditNoticeBtn');
            const adminNoticesList = document.getElementById('adminNoticesList');
            const noAdminNoticesMsg = document.getElementById('noAdminNotices');

            // LLM Elements (Student Dashboard - Memory Verse Explainer)
            const memoryVersesList = document.getElementById('memoryVersesList');
            const noStudentMemoryVerses = document.getElementById('noStudentMemoryVerses');
            const readMoreVersesBtn = document.getElementById('readMoreVersesBtn');


            // LLM Elements (Admin Dashboard - Lesson Plan Idea Generator)
            const lessonIdeaForm = document.getElementById('lessonIdeaForm');
            const lessonTopicInput = document.getElementById('lessonTopic');
            const lessonIdeasOutput = document.getElementById('lessonIdeasOutput');
            const lessonIdeasContent = document.getElementById('lessonIdeasContent');
            const lessonIdeasLoading = document.getElementById('lessonIdeasLoading');

            // Memory Verse Admin Elements
            const memoryVerseForm = document.getElementById('memoryVerseForm');
            const memoryVerseIdInput = document.getElementById('memoryVerseId');
            const memoryVerseTextInput = document.getElementById('memoryVerseText');
            const memoryVerseReferenceInput = document.getElementById('memoryVerseReference');
            const submitMemoryVerseBtn = document.getElementById('submitMemoryVerseBtn');
            const cancelEditMemoryVerseBtn = document.getElementById('cancelEditMemoryVerseBtn');
            const adminMemoryVersesList = document.getElementById('adminMemoryVersesList');
            const noAdminMemoryVersesMsg = document.getElementById('noAdminMemoryVerses');

            // NEW: Memory Verse Recitation Tracking (Admin)
            const recitationDateInput = document.getElementById('recitationDateInput');
            const adminViewSubJuniorRecitationBtn = document.getElementById('adminViewSubJuniorRecitationBtn');
            const adminSubJuniorRecitationContainer = document.getElementById('adminSubJuniorRecitationContainer');
            const subJuniorRecitationCheckboxes = document.getElementById('subJuniorRecitationCheckboxes');
            const adminSubJuniorRecitationForm = document.getElementById('adminSubJuniorRecitationForm');

            const adminViewJuniorRecitationBtn = document.getElementById('adminViewJuniorRecitationBtn');
            const adminJuniorRecitationContainer = document.getElementById('adminJuniorRecitationContainer');
            const juniorRecitationCheckboxes = document.getElementById('juniorRecitationCheckboxes');
            const adminJuniorRecitationForm = document.getElementById('adminJuniorRecitationForm');

            const adminViewSeniorRecitationBtn = document.getElementById('adminViewSeniorRecitationBtn');
            const adminSeniorRecitationContainer = document.getElementById('adminSeniorRecitationContainer');
            const seniorRecitationCheckboxes = document.getElementById('seniorRecitationCheckboxes');
            const adminSeniorRecitationForm = document.getElementById('adminSeniorRecitationForm');


            // Teacher Dashboard Specific Elements
            const teacherViewSubJuniorStudentsBtn = document.getElementById('teacherViewSubJuniorStudentsBtn');
            const teacherSubJuniorClassDetails = document.getElementById('teacherSubJuniorClassDetails');
            const teacherSubJuniorStudentsTableBody = document.getElementById('teacherSubJuniorStudentsTableBody');
            const teacherSubJuniorAttendanceForm = document.getElementById('teacherSubJuniorAttendanceForm');

            const teacherViewJuniorStudentsBtn = document.getElementById('teacherViewJuniorStudentsBtn');
            const teacherJuniorClassDetails = document.getElementById('teacherJuniorClassDetails');
            const teacherJuniorStudentsTableBody = document.getElementById('teacherJuniorStudentsTableBody');
            const teacherJuniorAttendanceForm = document.getElementById('teacherJuniorAttendanceForm');

            const teacherViewSeniorStudentsBtn = document.getElementById('teacherViewSeniorStudentsBtn');
            const teacherSeniorClassDetails = document.getElementById('teacherSeniorClassDetails');
            const teacherSeniorStudentsTableBody = document.getElementById('teacherSeniorStudentsTableBody');
            const teacherSeniorAttendanceForm = document.getElementById('teacherSeniorAttendanceForm');

            const teacherNoticesDisplay = document.getElementById('teacherNoticesDisplay');
            const noTeacherNotices = document.getElementById('noTeacherNotices');

            const teacherPendingLeaveApplicationsDiv = document.getElementById('teacherPendingLeaveApplications');
            const noTeacherPendingApplicationsMsg = document.getElementById('noTeacherPendingApplications');

            // Admin Dashboard Total Students Element
            const totalStudentsCountDisplay = document.getElementById('totalStudentsCount');

            // Downloads Centre Elements (User Dashboard)
            const userDownloadsList = document.getElementById('userDownloadsList');
            const noUserDownloadsMsg = document.getElementById('noUserDownloads');

            // Downloads Centre Elements (Admin Dashboard)
            const downloadForm = document.getElementById('downloadForm');
            const downloadIdInput = document.getElementById('downloadId');
            const downloadTitleInput = document.getElementById('downloadTitle');
            const downloadDescriptionInput = document.getElementById('downloadDescription');
            const downloadUrlInput = document.getElementById('downloadUrl');
            const downloadCategoryInput = document.getElementById('downloadCategory');
            const submitDownloadBtn = document.getElementById('submitDownloadBtn');
            const cancelEditDownloadBtn = document.getElementById('cancelEditDownloadBtn');
            const adminDownloadsList = document.getElementById('adminDownloadsList');
            const noAdminDownloadsMsg = document.getElementById('noAdminDownloads'); // Corrected from document = ...

            // Attendance Notification Admin Elements
            const attendanceNotificationsList = document.getElementById('attendanceNotificationsList');
            const noAttendanceNotificationsMsg = document.getElementById('noAttendanceNotifications');


            // Student Data (Moved to a central object for easier management)
            const studentData = {
                subJunior: [
                    { name: "Alice Smith", age: 3, mother: "Sarah Smith", father: "John Smith", phone: "555-1001" },
                    { name: "Bob Johnson", age: 4, mother: "Emily Johnson", father: "David Johnson", phone: "555-1002" },
                    { name: "Charlie Brown", age: 3, mother: "Lucy Brown", father: "Frank Brown", phone: "555-1003" },
                    { name: "Diana Green", age: 5, mother: "Laura Green", father: "Peter Green", phone: "555-1004" },
                    { name: "Ethan White", age: 4, mother: "Maria White", father: "Chris White", phone: "555-1005" },
                    { name: "Fiona Black", age: 3, mother: "Sophie Black", father: "Michael Black", phone: "555-1006" },
                    { name: "George King", age: 5, mother: "Olivia King", father: "Robert King", phone: "555-1007" },
                    { name: "Hannah Lee", age: 4, mother: "Grace Lee", father: "Kevin Lee", phone: "555-1008" },
                    { name: "Ian Clark", age: 3, mother: "Nancy Clark", father: "William Clark", phone: "555-1009" },
                    { name: "Julia Davis", age: 5, mother: "Megan Davis", father: "Mark Davis", phone: "555-1010" }
                ],
                junior: [
                    { name: "Olivia White", age: 6, mother: "Lisa White", father: "Paul White", phone: "555-2001" },
                    { name: "Noah Smith", age: 7, mother: "Karen Smith", father: "James Smith", phone: "555-2002" },
                    { name: "Emma Jones", age: 6, mother: "Nancy Jones", father: "Robert Jones", phone: "555-2003" },
                    { name: "Liam Brown", age: 8, mother: "Linda Brown", father: "Charles Brown", phone: "555-2004" },
                    { name: "Ava Garcia", age: 7, mother: "Brenda Garcia", father: "Jose Garcia", phone: "555-2005" },
                    { name: "Sophia Martinez", age: 6, mother: "Betty Martinez", father: "Carlos Martinez", phone: "555-2006" },
                    { name: "Jackson Rodriguez", age: 9, mother: "Maria Rodriguez", father: "Juan Rodriguez", phone: "555-2007" },
                    { name: "Mia Hernandez", age: 8, mother: "Patricia Hernandez", father: "Miguel Hernandez", phone: "555-2008" },
                    { name: "Lucas Lopez", age: 7, mother: "Susan Lopez", father: "Antonio Lopez", phone: "555-2009" },
                    { name: "Isabella Gonzalez", age: 10, mother: "Jessica Gonzalez", father: "Manuel Gonzalez", phone: "555-2010" }
                ],
                senior: [
                    { name: "Sophia Lee", age: 11, mother: "Grace Lee", father: "Kevin Lee", phone: "555-3001" },
                    { name: "Mason Davis", age: 12, mother: "Megan Davis", father: "Mark Davis", phone: "555-3002" },
                    { name: "Chloe Wilson", age: 13, mother: "Jessica Wilson", father: "Chris Wilson", phone: "555-3003" },
                    { name: "Logan Moore", age: 14, mother: "Michelle Moore", father: "Daniel Moore", phone: "555-3004" },
                    { name: "Abigail Taylor", age: 15, mother: "Amanda Taylor", father: "Paul Taylor", phone: "555-3005" },
                    { name: "Daniel Anderson", age: 16, mother: "Laura Anderson", father: "Sam Anderson", phone: "555-3006" },
                    { name: "Ella Thomas", age: 17, mother: "Olivia Thomas", father: "James Thomas", phone: "555-3007" },
                    { name: "Samuel Jackson", age: 11, mother: "Nicole Jackson", father: "Richard Jackson", phone: "555-3008" },
                    { name: "Grace White", age: 18, mother: "Hannah White", father: "Matthew White", phone: "555-3009" },
                    { name: "David Harris", age: 14, mother: "Sara Harris", father: "Chris Harris", phone: "555-3010" }
                ]
            };

            // Credentials
            const ADMIN_USERNAME = 'admin';
            const ADMIN_PASSWORD = 'adminpass';
            const TEACHER_USERNAME = 'teacher'; // New: Teacher username
            const TEACHER_PASSWORD = 'teacherpass'; // New: Teacher password

            // Initialize USERS object with static and dynamic users
            const USERS = {
                'sunday': 'school', // Original generic user (student)
                [ADMIN_USERNAME]: ADMIN_PASSWORD, // Admin user
                [TEACHER_USERNAME]: TEACHER_PASSWORD // Teacher user
            };

            // Dynamically add student users to the USERS object
            function addStudentUsers() {
                for (const grade in studentData) {
                    studentData[grade].forEach(student => {
                        // Create a simple username from the student's name
                        const username = student.name.toLowerCase().replace(/\s/g, '');
                        USERS[username] = 'studentpass'; // Assign a generic password for all students
                    });
                }
            }
            addStudentUsers(); // Call this function to populate USERS object on load

            // Utility to get current date inYYYY-MM-DD format
            function getCurrentDateFormatted() {
                const today = new Date();
                const year = today.getFullYear();
                const month = String(today.getMonth() + 1).padStart(2, '0'); // Months are 0-indexed
                const day = String(today.getDate()).padStart(2, '0');
                return `${year}-${month}-${day}`;
            }

            // Set default date for recitationDateInput to today
            if (recitationDateInput) {
                recitationDateInput.value = getCurrentDateFormatted();
            }

            // Function to show modal
            function showLoginModal() {
                modalTitle.textContent = 'Canaan Sunday School Login'; // Generic title
                loginModal.classList.add('show');
                usernameInput.value = '';
                passwordInput.value = '';
                loginMessage.classList.add('hidden');
                usernameInput.focus();
            }

            // Function to hide modal
            function hideLoginModal() {
                loginModal.classList.remove('show');
            }

            // Function to reset all content visibility to public content
            function showPublicContent() {
                mainContent.classList.remove('hidden');
                userDashboard.classList.add('hidden');
                adminDashboard.classList.add('hidden');
                teacherDashboard.classList.add('hidden'); // New: Hide teacher dashboard

                loginButtonNav.classList.remove('hidden');
                logoutNavItem.classList.add('hidden');
            }

            // Event Listeners for Nav Buttons
            if (loginButtonNav) {
                loginButtonNav.addEventListener('click', () => showLoginModal());
            }
            if (closeModalBtn) {
                closeModalBtn.addEventListener('click', hideLoginModal);
            }
            if (loginModal) {
                loginModal.addEventListener('click', function(event) {
                    if (event.target === loginModal) {
                        hideLoginModal();
                    }
                });
            }
            if (logoutBtn) {
                logoutBtn.addEventListener('click', showPublicContent);
            }

            // Function to fetch and display student's attendance
            async function fetchAndDisplayStudentAttendance(username) {
                if (!db) {
                    studentAttendanceStatusDiv.textContent = "Attendance system unavailable (Firebase not initialized).";
                    console.error("Firestore DB is not initialized.");
                    return;
                }
                studentAttendanceStatusDiv.textContent = "Checking attendance...";
                const todayDate = getCurrentDateFormatted();
                // Public data collection
                const attendanceDocRef = doc(db, `artifacts/${appId}/public/data/dailyAttendance`, todayDate);

                try {
                    const docSnap = await getDoc(attendanceDocRef);
                    if (docSnap.exists()) {
                        const dailyAttendance = docSnap.data();
                        const studentStatus = dailyAttendance[username]; // Check by username (lowercase, no spaces)

                        if (studentStatus === true) {
                            studentAttendanceStatusDiv.textContent = "Status: Present";
                            studentAttendanceStatusDiv.className = "text-center text-xl font-semibold text-green-700";
                        } else if (studentStatus === false) {
                            studentAttendanceStatusDiv.textContent = "Status: Absent";
                            studentAttendanceStatusDiv.className = "text-center text-xl font-semibold text-red-700";
                        } else {
                            studentAttendanceStatusDiv.textContent = "Status: Not recorded for today.";
                            studentAttendanceStatusDiv.className = "text-center text-xl font-semibold text-gray-800";
                        }
                    } else {
                        studentAttendanceStatusDiv.textContent = "No attendance record found for today.";
                        studentAttendanceStatusDiv.className = "text-center text-xl font-semibold text-gray-800";
                    }
                } catch (error) {
                    console.error("Error fetching student attendance:", error);
                    studentAttendanceStatusDiv.textContent = "Error fetching attendance.";
                    studentAttendanceStatusDiv.className = "text-center text-xl font-semibold text-red-500";
                }
            }

            // NEW: Function to fetch and display student's memory verse recitation status
            async function fetchAndDisplayUserRecitationStatus(username) {
                if (!db) {
                    userRecitationStatusDiv.textContent = "Recitation status system unavailable (Firebase not initialized).";
                    console.error("Firestore DB is not initialized.");
                    return;
                }
                userRecitationStatusDiv.textContent = "Checking recitation status...";
                const todayDate = getCurrentDateFormatted();
                const recitationDocRef = doc(db, `artifacts/${appId}/public/data/dailyMemoryVerseRecitations`, todayDate);

                try {
                    const docSnap = await getDoc(recitationDocRef);
                    if (docSnap.exists()) {
                        const dailyRecitations = docSnap.data();
                        const recitationStatus = dailyRecitations[username];

                        if (recitationStatus === true) {
                            userRecitationStatusDiv.textContent = "Status: You have recited the memory verse today! ✅";
                            userRecitationStatusDiv.className = "text-center text-xl font-semibold text-green-700";
                        } else if (recitationStatus === false) {
                            userRecitationStatusDiv.textContent = "Status: You have not recited the memory verse today. ❌";
                            userRecitationStatusDiv.className = "text-center text-xl font-semibold text-red-700";
                        } else {
                            userRecitationStatusDiv.textContent = "Status: Recitation not yet marked for today.";
                            userRecitationStatusDiv.className = "text-center text-xl font-semibold text-gray-800";
                        }
                    } else {
                        userRecitationStatusDiv.textContent = "No recitation record found for today.";
                        userRecitationStatusDiv.className = "text-center text-xl font-semibold text-gray-800";
                    }
                } catch (error) {
                    console.error("Error fetching user recitation status:", error);
                    userRecitationStatusDiv.textContent = "Error fetching recitation status.";
                    userRecitationStatusDiv.className = "text-center text-xl font-semibold text-red-500";
                }
            }


            // Function to fetch and display student's leave applications
            async function fetchAndDisplayLeaveApplications(userId) {
                if (!db) {
                    pastLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center text-red-500">Leave application system unavailable (Firebase not initialized).</p>';
                    return;
                }

                pastLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center">Loading past applications...</p>';
                const leaveApplicationsCollectionRef = collection(db, `artifacts/${appId}/users/${userId}/leaveApplications`);
                
                try {
                    const q = query(leaveApplicationsCollectionRef);
                    const querySnapshot = await getDocs(q);

                    if (querySnapshot.empty) {
                        pastLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center" id="noPastApplications">No past leave applications found.</p>';
                        noPastApplicationsMsg.classList.remove('hidden'); // Ensure message is visible
                    } else {
                        noPastApplicationsMsg.classList.add('hidden'); // Hide message if applications exist
                        const applications = [];
                        querySnapshot.forEach(doc => {
                            applications.push({ id: doc.id, ...doc.data() });
                        });

                        // Sort applications by submissionTimestamp (most recent first) in memory
                        applications.sort((a, b) => {
                            // Convert Firestore Timestamp to Date objects for comparison
                            const dateA = a.submissionTimestamp ? a.submissionTimestamp.toDate() : new Date(a.submissionDate);
                            const dateB = b.submissionTimestamp ? b.submissionTimestamp.toDate() : new Date(b.submissionDate);
                            return dateB - dateA;
                        });

                        pastLeaveApplicationsDiv.innerHTML = ''; // Clear loading message

                        applications.forEach(app => {
                            const appElement = document.createElement('div');
                            appElement.classList.add('bg-blue-50', 'p-4', 'rounded-lg', 'shadow-sm', 'border-l-4');
                            // Dynamic border color based on status
                            if (app.status === 'Approved') {
                                appElement.classList.add('border-green-500');
                            } else if (app.status === 'Disapproved') {
                                appElement.classList.add('border-red-500');
                            } else {
                                appElement.classList.add('border-blue-500'); // Pending
                            }

                            appElement.innerHTML = `
                                <p class="text-md font-semibold text-blue-800 mb-1">Reason: ${app.reason}</p>
                                <p class="text-sm text-gray-700 mb-1">From: ${app.startDate} To: ${app.endDate}</p>
                                <p class="text-xs text-gray-500">Submitted: ${new Date(app.submissionDate).toLocaleString()}</p>
                                <p class="text-sm font-bold mt-2">Status: <span class="${app.status === 'Approved' ? 'text-green-600' : (app.status === 'Disapproved' ? 'text-red-600' : 'text-yellow-600')}">${app.status}</span></p>
                            `;
                            pastLeaveApplicationsDiv.appendChild(appElement);
                        });
                    }
                } catch (error) {
                    console.error("Error fetching leave applications:", error);
                    pastLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center text-red-500">Error loading past applications.</p>';
                }
            }


            // Handle Login Form Submission - Unified Logic
            if (loginForm) {
                loginForm.addEventListener('submit', async function(event) {
                    event.preventDefault();
                    currentUsername = usernameInput.value; // Store the logged-in username
                    const enteredPassword = passwordInput.value;

                    // Check if provided credentials match any defined user
                    if (USERS[currentUsername] === enteredPassword) {
                        hideLoginModal();
                        mainContent.classList.add('hidden');
                        loginButtonNav.classList.add('hidden');
                        logoutNavItem.classList.remove('hidden');

                        if (currentUsername === ADMIN_USERNAME) {
                            userDashboard.classList.add('hidden'); // Ensure user dashboard is hidden
                            teacherDashboard.classList.add('hidden'); // Ensure teacher dashboard is hidden
                            adminDashboard.classList.remove('hidden');
                            await displayTotalPresentStudentsCount(); // Display total present students for admin
                            await fetchAndDisplayAdminLeaveApplications(); // Load pending applications for admin
                            setupAdminNoticesListener(); // Setup admin notices listener
                            setupAdminMemoryVersesListener(); // Setup admin memory verses listener
                            setupAdminDownloadsListener(); // Setup admin downloads listener
                            setupAdminAttendanceNotificationsListener(); // Setup admin attendance notifications listener
                        } else if (currentUsername === TEACHER_USERNAME) { // New: Teacher login
                            userDashboard.classList.add('hidden');
                            adminDashboard.classList.add('hidden');
                            teacherDashboard.classList.remove('hidden');
                            // Fetch and display teacher-specific data
                            setupTeacherNoticesListener();
                            await fetchAndDisplayTeacherLeaveApplications();
                        }
                        else {
                            // Regular user or student login successful
                            adminDashboard.classList.add('hidden'); // Ensure admin dashboard is hidden
                            teacherDashboard.classList.add('hidden'); // Ensure teacher dashboard is hidden
                            userDashboard.classList.remove('hidden');
                            if (dashboardUsernameSpan) {
                                dashboardUsernameSpan.textContent = currentUsername;
                            }
                            await fetchAndDisplayStudentAttendance(currentUsername); // Fetch and display attendance for student
                            await fetchAndDisplayUserRecitationStatus(currentUsername); // NEW: Fetch and display recitation status for student
                            
                            if (auth.currentUser) { // Ensure Firebase user is authenticated
                                await fetchAndDisplayLeaveApplications(auth.currentUser.uid);
                            } else {
                                console.warn("Cannot fetch leave applications: User not authenticated.");
                                pastLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center text-red-500">User not authenticated. Cannot load leave applications.</p>';
                            }
                            setupStudentNoticesListener(); // Setup student notices listener
                            setupStudentMemoryVersesListener(); // Setup student memory verses listener
                            setupUserDownloadsListener(); // Setup user downloads listener
                        }
                    } else {
                        loginMessage.classList.remove('hidden');
                    }
                });
            }

            // Handle Leave Application Form Submission
            if (leaveApplicationForm) {
                leaveApplicationForm.addEventListener('submit', async function(event) {
                    event.preventDefault();

                    if (!db || !auth.currentUser) {
                        showMessageBox("Error", "Please log in to submit a leave application.");
                        return;
                    }

                    const startDate = leaveStartDateInput.value;
                    const endDate = leaveEndDateInput.value;
                    const reason = leaveReasonInput.value.trim();
                    
                    // Get student's full name from studentData based on currentUsername
                    let studentFullName = currentUsername; // Default to username if not found
                    for (const grade in studentData) {
                        const foundStudent = studentData[grade].find(s => s.name.toLowerCase().replace(/\s/g, '') === currentUsername);
                        if (foundStudent) {
                            studentFullName = foundStudent.name;
                            break;
                        }
                    }


                    // Basic date validation
                    if (new Date(startDate) > new Date(endDate)) {
                        showMessageBox("Error", "End date cannot be before start date.");
                        return;
                    }
                    if (reason === "") {
                        showMessageBox("Error", "Please provide a reason for your leave.");
                        return;
                    }

                    const userId = auth.currentUser.uid;
                    const privateLeaveAppCollectionRef = collection(db, `artifacts/${appId}/users/${userId}/leaveApplications`);
                    const publicLeaveAppInboxRef = collection(db, `artifacts/${appId}/public/data/leaveApplicationsInbox`);

                    try {
                        // 1. Add to private collection (to get the private doc ID)
                        const privateDocRef = doc(privateLeaveAppCollectionRef); // Create a new doc reference with auto ID
                        await setDoc(privateDocRef, {
                            startDate: startDate,
                            endDate: endDate,
                            reason: reason,
                            submissionDate: new Date().toISOString(), // Store as ISO string
                            submissionTimestamp: serverTimestamp(), // Store as Firestore Timestamp for sorting
                            status: "Pending" // Initial status
                        });

                        // 2. Add to public inbox with reference to the private document and student details
                        await setDoc(doc(publicLeaveAppInboxRef), {
                            studentId: userId,
                            studentUsername: currentUsername,
                            studentFullName: studentFullName,
                            privateDocId: privateDocRef.id, // Store the ID of the private document
                            startDate: startDate,
                            endDate: endDate,
                            reason: reason,
                            submissionDate: new Date().toISOString(), // Use ISO string for display
                            submissionTimestamp: serverTimestamp(), // Use Firestore Timestamp for sorting
                            status: "Pending"
                        });

                        showMessageBox("Success", "Leave application submitted successfully!");
                        leaveApplicationForm.reset(); // Clear the form
                        await fetchAndDisplayLeaveApplications(userId); // Refresh past applications list
                    } catch (error) {
                        console.error("Error submitting leave application:", error);
                        showMessageBox("Error", "Failed to submit leave application. Please try again.");
                    }
                });
            }


            // ADMIN DASHBOARD SPECIFIC FUNCTIONALITY - Dynamic Table and Attendance Forms

            // Function to calculate and display total PRESENT students
            async function displayTotalPresentStudentsCount() {
                if (!db) {
                    totalStudentsCountDisplay.textContent = "N/A";
                    console.error("Firestore DB is not initialized. Cannot display present count.");
                    return;
                }

                totalStudentsCountDisplay.textContent = "Loading...";
                const todayDate = getCurrentDateFormatted();
                const attendanceDocRef = doc(db, `artifacts/${appId}/public/data/dailyAttendance`, todayDate);

                try {
                    const docSnap = await getDoc(attendanceDocRef);
                    let presentCount = 0;
                    if (docSnap.exists()) {
                        const dailyAttendance = docSnap.data();
                        for (const studentKey in dailyAttendance) {
                            if (dailyAttendance[studentKey] === true) {
                                presentCount++;
                            }
                        }
                    }
                    totalStudentsCountDisplay.textContent = presentCount;
                } catch (error) {
                    console.error("Error fetching total present students:", error);
                    totalStudentsCountDisplay.textContent = "Error";
                    showMessageBox("Error", "Could not load total present students.");
                }
            }


            function populateStudentTable(grade, tableBodyId) {
                const tableBody = document.getElementById(tableBodyId);
                if (!tableBody) return; // Exit if element not found
                tableBody.innerHTML = ''; // Clear existing rows

                studentData[grade].forEach((student, index) => {
                    const row = document.createElement('tr');
                    row.classList.add('border-b', 'border-gray-200');
                    if (index % 2 !== 0) { // Add stripy effect for odd rows
                        row.classList.add('bg-gray-50');
                    }
                    row.innerHTML = `
                        <td class="py-2 px-4 text-gray-800">${student.name}</td>
                        <td class="py-2 px-4 text-gray-800">${student.age}</td>
                        <td class="py-2 px-4 text-gray-800">${student.mother}</td>
                        <td class="py-2 px-4 text-gray-800">${student.father}</td>
                        <td class="py-2 px-4 text-gray-800">${student.phone}</td>
                    `;
                    tableBody.appendChild(row);
                });
            }

            async function populateAttendanceCheckboxes(grade, checkboxesContainerElement, formId, isTeacher = false) {
                const checkboxesContainer = checkboxesContainerElement;
                if (!checkboxesContainer) return;
                checkboxesContainer.innerHTML = ''; // Clear existing checkboxes

                const todayDate = getCurrentDateFormatted();
                let existingAttendance = {};
                if (db) {
                    try {
                        const attendanceDocRef = doc(db, `artifacts/${appId}/public/data/dailyAttendance`, todayDate);
                        const docSnap = await getDoc(attendanceDocRef);
                        if (docSnap.exists()) {
                            existingAttendance = docSnap.data();
                        }
                    } catch (error) {
                        console.error("Error fetching existing attendance:", error);
                        showMessageBox("Error", "Could not load previous attendance records.");
                    }
                }

                studentData[grade].forEach(student => {
                    const username = student.name.toLowerCase().replace(/\s/g, '');
                    const isPresent = existingAttendance[username] === true; // Default to false if not in record

                    // If it's a teacher's view, we populate a table row instead of standalone checkboxes
                    if (isTeacher) {
                        const row = document.createElement('tr');
                        row.classList.add('border-b', 'border-gray-200');
                        row.innerHTML = `
                            <td class="py-2 px-4 text-gray-800">${student.name}</td>
                            <td class="py-2 px-4 text-gray-800">${student.age}</td>
                            <td class="py-2 px-4 text-gray-800">
                                <input type="checkbox" name="attendance" value="${username}" ${isPresent ? 'checked' : ''} class="form-checkbox h-5 w-5 text-green-600 rounded">
                            </td>
                        `;
                        checkboxesContainer.appendChild(row); // 'checkboxesContainer' is actually a tbody for teachers
                    } else {
                        // Admin view, uses labels and inputs directly
                        const label = document.createElement('label');
                        label.classList.add('flex', 'items-center', 'space-x-2');
                        label.innerHTML = `
                            <input type="checkbox" name="attendance" value="${username}" ${isPresent ? 'checked' : ''} class="form-checkbox h-5 w-5 text-blue-600 rounded">
                            <span class="text-gray-800">${student.name}</span>
                        `;
                        checkboxesContainer.appendChild(label);
                    }
                });

                // Attach submit listener to the form
                const form = document.getElementById(formId);
                if (form) {
                    // Remove existing listener to prevent duplicates
                    form.removeEventListener('submit', (event) => handleAttendanceSubmit(event, grade));
                    form.addEventListener('submit', (event) => handleAttendanceSubmit(event, grade));
                }
            }


            async function handleAttendanceSubmit(event, grade) {
                event.preventDefault();
                if (!db) {
                    showMessageBox("Error", "Attendance system unavailable (Firebase not initialized).");
                    return;
                }

                const form = event.target;
                const checkboxes = form.querySelectorAll('input[name="attendance"]');
                const todayDate = getCurrentDateFormatted();
                const attendanceUpdates = {};

                checkboxes.forEach(checkbox => {
                    // Use username (lowercase, no spaces) as key for consistency
                    attendanceUpdates[checkbox.value] = checkbox.checked;
                });

                const attendanceDocRef = doc(db, `artifacts/${appId}/public/data/dailyAttendance`, todayDate);

                try {
                    await setDoc(attendanceDocRef, attendanceUpdates, { merge: true }); // Merge to update only checked students
                    showMessageBox("Success", `Attendance recorded for ${grade} for ${todayDate}!`);
                    
                    // --- NEW: Send notification to admin dashboard ---
                    const attendanceNotificationsCollectionRef = collection(db, `artifacts/${appId}/public/data/attendanceNotifications`);
                    await addDoc(attendanceNotificationsCollectionRef, {
                        grade: grade,
                        date: todayDate,
                        submittedBy: currentUsername, // The user who submitted (teacher or admin)
                        submissionTimestamp: serverTimestamp(),
                        status: "Pending" // Initial status for review
                    });
                    // --- END NEW ---

                    // Update the total present students count in admin dashboard after attendance submission
                    if (currentUsername === ADMIN_USERNAME) {
                        await displayTotalPresentStudentsCount();
                    }
                    // Reset form checkboxes after submission (optional, can be re-populated on next open)
                    // checkboxes.forEach(checkbox => checkbox.checked = false);
                } catch (error) {
                    console.error("Error submitting attendance:", error);
                    showMessageBox("Error", "Failed to record attendance. Please try again.");
                }
            }

            // Admin Sub Junior
            const adminViewSubJuniorStudentsBtn = document.getElementById('adminViewSubJuniorStudentsBtn');
            const adminSubJuniorStudentsTableContainer = document.getElementById('adminSubJuniorStudentsTableContainer');
            const adminMarkSubJuniorAttendanceBtn = document.getElementById('adminMarkSubJuniorAttendanceBtn');
            const adminSubJuniorAttendanceFormContainer = document.getElementById('adminSubJuniorAttendanceFormContainer');
            
            if (adminViewSubJuniorStudentsBtn && adminSubJuniorStudentsTableContainer) {
                adminViewSubJuniorStudentsBtn.addEventListener('click', function() {
                    adminSubJuniorStudentsTableContainer.classList.toggle('hidden');
                    if (!adminSubJuniorStudentsTableContainer.classList.contains('hidden')) {
                        populateStudentTable('subJunior', 'subJuniorStudentsTableBody');
                        adminViewSubJuniorStudentsBtn.textContent = 'Hide Sub Junior Students';
                    } else {
                        adminSubJuniorStudentsTableContainer.classList.add('hidden'); // Ensure hidden on subsequent clicks
                        adminViewSubJuniorStudentsBtn.textContent = 'View Sub Junior Students';
                    }
                });
            }
            if (adminMarkSubJuniorAttendanceBtn && adminSubJuniorAttendanceFormContainer) {
                adminMarkSubJuniorAttendanceBtn.addEventListener('click', function() {
                    adminSubJuniorAttendanceFormContainer.classList.toggle('hidden');
                    if (!adminSubJuniorAttendanceFormContainer.classList.contains('hidden')) {
                        // Pass the container element directly for admin
                        populateAttendanceCheckboxes('subJunior', document.getElementById('subJuniorAttendanceCheckboxes'), 'adminSubJuniorAttendanceForm');
                        adminMarkSubJuniorAttendanceBtn.textContent = 'Hide Sub Junior Attendance Form';
                    } else {
                        adminMarkSubJuniorAttendanceBtn.textContent = 'Mark Sub Junior Attendance';
                    }
                });
            }

            // Admin Junior
            const adminViewJuniorStudentsBtn = document.getElementById('adminViewJuniorStudentsBtn');
            const adminJuniorStudentsTableContainer = document.getElementById('adminJuniorStudentsTableContainer');
            const adminMarkJuniorAttendanceBtn = document.getElementById('adminMarkJuniorAttendanceBtn');
            const adminJuniorAttendanceFormContainer = document.getElementById('adminJuniorAttendanceFormContainer');

            if (adminViewJuniorStudentsBtn && adminJuniorStudentsTableContainer) {
                adminViewJuniorStudentsBtn.addEventListener('click', function() {
                    adminJuniorStudentsTableContainer.classList.toggle('hidden');
                    if (!adminJuniorStudentsTableContainer.classList.contains('hidden')) {
                        populateStudentTable('junior', 'juniorStudentsTableBody');
                        adminViewJuniorStudentsBtn.textContent = 'Hide Junior Students';
                    } else {
                        adminJuniorStudentsTableContainer.classList.add('hidden'); // Ensure hidden on subsequent clicks
                        adminViewJuniorStudentsBtn.textContent = 'View Junior Students';
                    }
                });
            }
            if (adminMarkJuniorAttendanceBtn && adminJuniorAttendanceFormContainer) {
                adminMarkJuniorAttendanceBtn.addEventListener('click', function() {
                    adminJuniorAttendanceFormContainer.classList.toggle('hidden');
                    if (!adminJuniorAttendanceFormContainer.classList.contains('hidden')) {
                        populateAttendanceCheckboxes('junior', document.getElementById('juniorAttendanceCheckboxes'), 'adminJuniorAttendanceForm');
                        adminMarkJuniorAttendanceBtn.textContent = 'Hide Junior Attendance Form';
                    } else {
                        adminJuniorAttendanceBtn.textContent = 'Mark Junior Attendance';
                    }
                    if (adminJuniorStudentsTableContainer) { // Also hide table if attendance form is shown
                        adminJuniorStudentsTableContainer.classList.add('hidden');
                        adminViewJuniorStudentsBtn.textContent = 'View Junior Students';
                    }
                });
            }

            // Admin Senior
            const adminViewSeniorStudentsBtn = document.getElementById('adminViewSeniorStudentsBtn');
            const adminSeniorStudentsTableContainer = document.getElementById('adminSeniorStudentsTableContainer');
            const adminMarkSeniorAttendanceBtn = document.getElementById('adminMarkSeniorAttendanceBtn');
            const adminSeniorAttendanceFormContainer = document.getElementById('adminSeniorAttendanceFormContainer');

            if (adminViewSeniorStudentsBtn && adminSeniorStudentsTableContainer) {
                adminViewSeniorStudentsBtn.addEventListener('click', function() {
                    adminSeniorStudentsTableContainer.classList.toggle('hidden');
                    if (!adminSeniorStudentsTableContainer.classList.contains('hidden')) {
                        populateStudentTable('senior', 'seniorStudentsTableBody');
                        adminViewSeniorStudentsBtn.textContent = 'Hide Senior Students';
                    } else {
                        adminSeniorStudentsTableContainer.classList.add('hidden'); // Ensure hidden on subsequent clicks
                        adminViewSeniorStudentsBtn.textContent = 'View Senior Students';
                    }
                });
            }
            if (adminMarkSeniorAttendanceBtn && adminSeniorAttendanceFormContainer) {
                adminMarkSeniorAttendanceBtn.addEventListener('click', function() {
                    adminSeniorAttendanceFormContainer.classList.toggle('hidden');
                    if (!adminSeniorAttendanceFormContainer.classList.contains('hidden')) {
                        populateAttendanceCheckboxes('senior', document.getElementById('seniorAttendanceCheckboxes'), 'adminSeniorAttendanceForm');
                        adminMarkSeniorAttendanceBtn.textContent = 'Hide Senior Attendance Form';
                    } else {
                        adminSeniorAttendanceBtn.textContent = 'Mark Senior Attendance';
                    }
                    if (adminSeniorStudentsTableContainer) { // Also hide table if attendance form is shown
                        adminSeniorStudentsTableContainer.classList.add('hidden');
                        adminViewSeniorStudentsBtn.textContent = 'View Senior Students';
                    }
                });
            }

            // Admin Leave Application Management Functions
            async function fetchAndDisplayAdminLeaveApplications() {
                if (!db) {
                    pendingLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center text-red-500">Leave application management unavailable (Firebase not initialized).</p>';
                    return;
                }

                pendingLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center">Loading pending applications...</p>';
                const publicLeaveAppInboxRef = collection(db, `artifacts/${appId}/public/data/leaveApplicationsInbox`);
                
                try {
                    // Query for applications with status 'Pending'
                    const q = query(publicLeaveAppInboxRef, where("status", "==", "Pending"));
                    const querySnapshot = await getDocs(q);

                    if (querySnapshot.empty) {
                        pendingLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center" id="noPendingApplications">No pending leave applications.</p>';
                        noPendingApplicationsMsg.classList.remove('hidden');
                    } else {
                        noPendingApplicationsMsg.classList.add('hidden');
                        pendingLeaveApplicationsDiv.innerHTML = ''; // Clear loading message

                        querySnapshot.forEach(appDoc => {
                            const appData = appDoc.data();
                            const appElement = document.createElement('div');
                            appElement.classList.add('bg-purple-50', 'p-4', 'rounded-lg', 'shadow-sm', 'border-l-4', 'border-purple-500', 'flex', 'flex-col', 'md:flex-row', 'md:items-center', 'md:justify-between', 'space-y-3', 'md:space-y-0');
                            
                            // Using appData.studentFullName for display
                            const studentInfo = appData.studentFullName || appData.studentUsername || "Unknown Student";

                            appElement.innerHTML = `
                                <div>
                                    <p class="text-md font-semibold text-purple-800 mb-1">Student: ${studentInfo}</p>
                                    <p class="text-sm text-gray-700 mb-1">Reason: ${appData.reason}</p>
                                    <p class="text-xs text-gray-600">From: ${appData.startDate} To: ${appData.endDate}</p>
                                    <p class="text-xs text-gray-500">Submitted: ${new Date(appData.submissionDate).toLocaleString()}</p>
                                </div>
                                <div class="flex space-x-2">
                                    <button class="approve-btn bg-green-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-green-600 transition-all-ease" data-public-doc-id="${appDoc.id}" data-student-id="${appData.studentId}" data-private-doc-id="${appData.privateDocId}">Approve</button>
                                    <button class="disapprove-btn bg-red-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-red-600 transition-all-ease" data-public-doc-id="${appDoc.id}" data-student-id="${appData.studentId}" data-private-doc-id="${appData.privateDocId}">Disapprove</button>
                                </div>
                            `;
                            pendingLeaveApplicationsDiv.appendChild(appElement);
                        });

                        // Attach event listeners to the new buttons
                        pendingLeaveApplicationsDiv.querySelectorAll('.approve-btn').forEach(button => {
                            button.addEventListener('click', handleLeaveAction);
                        });
                        pendingLeaveApplicationsDiv.querySelectorAll('.disapprove-btn').forEach(button => {
                            button.addEventListener('click', handleLeaveAction);
                        });

                    }
                } catch (error) {
                    console.error("Error fetching admin leave applications:", error);
                    showMessageBox("Error", "Failed to load pending leave applications.");
                }
            }

            async function handleLeaveAction(event) {
                if (!db) {
                    showMessageBox("Error", "Database not connected. Cannot perform action.");
                    return;
                }

                const button = event.target;
                const publicDocId = button.dataset.publicDocId;
                const studentId = button.dataset.studentId;
                const privateDocId = button.dataset.privateDocId;
                const action = button.classList.contains('approve-btn') ? 'Approved' : 'Disapproved';

                if (!publicDocId || !studentId || !privateDocId) {
                    console.error("Missing data attributes for leave action:", { publicDocId, studentId, privateDocId });
                    showMessageBox("Error", "Missing application data. Cannot process request.");
                    return;
                }

                const publicDocRef = doc(db, `artifacts/${appId}/public/data/leaveApplicationsInbox`, publicDocId);
                const privateDocRef = doc(db, `artifacts/${appId}/users/${studentId}/leaveApplications`, privateDocId);

                try {
                    // Update status in public inbox
                    await updateDoc(publicDocRef, { status: action });
                    // Update status in student's private collection
                    await updateDoc(privateDocRef, { status: action });

                    showMessageBox("Success", `Leave application ${action.toLowerCase()}!`);
                    // Refresh view based on current dashboard (admin or teacher)
                    if (adminDashboard.classList.contains('hidden')) { // If teacher dashboard is active
                        await fetchAndDisplayTeacherLeaveApplications();
                    } else { // If admin dashboard is active
                        await fetchAndDisplayAdminLeaveApplications(); 
                    }
                } catch (error) {
                    console.error(`Error ${action.toLowerCase()} leave application:`, error);
                    showMessageBox("Error", `Failed to ${action.toLowerCase()} leave application. Please try again.`);
                }
            }

            // Notice Board Management (Admin Side)
            let unsubscribeNotices = null; // To store the unsubscribe function for real-time listener

            function setupAdminNoticesListener() {
                if (!db || unsubscribeNotices) return; // Prevent multiple listeners

                const noticesCollectionRef = collection(db, `artifacts/${appId}/public/data/notices`);
                const q = query(noticesCollectionRef); // Removed orderBy as per instructions, will sort in memory

                unsubscribeNotices = onSnapshot(q, (snapshot) => {
                    const notices = [];
                    snapshot.forEach(doc => {
                        notices.push({ id: doc.id, ...doc.data() });
                    });

                    // Sort notices by creation timestamp (most recent first)
                    notices.sort((a, b) => {
                        const dateA = a.timestamp ? a.timestamp.toDate() : new Date(0); // Fallback for old data without timestamp
                        const dateB = b.timestamp ? b.timestamp.toDate() : new Date(0);
                        return dateB - dateA;
                    });

                    renderAdminNotices(notices);
                }, (error) => {
                    console.error("Error listening to notices:", error);
                    adminNoticesList.innerHTML = '<p class="text-red-600 text-center">Error loading notices.</p>';
                    noAdminNoticesMsg.classList.remove('hidden');
                });
            }

            function renderAdminNotices(notices) {
                if (notices.length === 0) {
                    adminNoticesList.innerHTML = '<p class="text-gray-600 text-center" id="noAdminNotices">No notices currently posted.</p>';
                    noAdminNoticesMsg.classList.remove('hidden');
                } else {
                    noAdminNoticesMsg.classList.add('hidden');
                    adminNoticesList.innerHTML = '';
                    notices.forEach(notice => {
                        const noticeElement = document.createElement('div');
                        noticeElement.classList.add('bg-gray-50', 'p-4', 'rounded-lg', 'shadow-sm', 'border-l-4', 'border-blue-400', 'flex', 'flex-col', 'md:flex-row', 'md:items-center', 'md:justify-between', 'space-y-2', 'md:space-y-0');
                        
                        const date = notice.timestamp ? new Date(notice.timestamp.toDate()).toLocaleString() : 'N/A';

                        noticeElement.innerHTML = `
                            <div>
                                <h4 class="text-lg font-semibold text-gray-800">${notice.title}</h4>
                                <p class="text-gray-700 text-sm">${notice.content}</p>
                                <p class="text-xs text-gray-500 mt-1">Posted: ${date}</p>
                            </div>
                            <div class="flex space-x-2">
                                <button class="edit-notice-btn bg-yellow-500 text-white font-semibold py-1 px-3 rounded-full text-sm shadow-md hover:bg-yellow-600 transition-all-ease" data-id="${notice.id}" data-title="${encodeURIComponent(notice.title)}" data-content="${encodeURIComponent(notice.content)}">Edit</button>
                                <button class="delete-notice-btn bg-red-500 text-white font-semibold py-1 px-3 rounded-full text-sm shadow-md hover:bg-red-600 transition-all-ease" data-id="${notice.id}">Delete</button>
                            </div>
                        `;
                        adminNoticesList.appendChild(noticeElement);
                    });

                    // Attach event listeners for edit and delete buttons
                    adminNoticesList.querySelectorAll('.edit-notice-btn').forEach(button => {
                        button.addEventListener('click', (e) => {
                            const id = e.target.dataset.id;
                            const title = decodeURIComponent(e.target.dataset.title);
                            const content = decodeURIComponent(e.target.dataset.content);
                            
                            noticeIdInput.value = id;
                            noticeTitleInput.value = title;
                            noticeContentInput.value = content;
                            submitNoticeBtn.textContent = 'Update Notice';
                            submitNoticeBtn.classList.remove('bg-blue-600', 'hover:bg-blue-700');
                            submitNoticeBtn.classList.add('bg-green-600', 'hover:bg-green-700');
                            cancelEditNoticeBtn.classList.remove('hidden');
                        });
                    });
                    adminNoticesList.querySelectorAll('.delete-notice-btn').forEach(button => {
                        button.addEventListener('click', async (e) => {
                            const id = e.target.dataset.id;
                            if (confirm("Are you sure you want to delete this notice?")) { // Use browser confirm for simplicity in admin panel
                                await deleteNotice(id);
                            }
                        });
                    });
                }
            }

            if (noticeForm) {
                noticeForm.addEventListener('submit', async (e) => {
                    e.preventDefault();
                    if (!db) {
                        showMessageBox("Error", "Notice board system unavailable (Firebase not initialized).");
                        return;
                    }

                    const id = noticeIdInput.value;
                    const title = noticeTitleInput.value.trim();
                    const content = noticeContentInput.value.trim();

                    if (!title || !content) {
                        showMessageBox("Validation Error", "Please fill in both title and content for the notice.");
                        return;
                    }

                    const noticesCollectionRef = collection(db, `artifacts/${appId}/public/data/notices`);

                    try {
                        if (id) { // Editing existing notice
                            const noticeDocRef = doc(noticesCollectionRef, id);
                            await updateDoc(noticeDocRef, { title, content, timestamp: serverTimestamp() });
                            showMessageBox("Success", "Notice updated successfully!");
                        } else { // Adding new notice
                            await addDoc(noticesCollectionRef, { title, content, timestamp: serverTimestamp() });
                            showMessageBox("Success", "Notice added successfully!");
                        }
                        noticeForm.reset();
                        noticeIdInput.value = ''; // Clear hidden ID
                        submitNoticeBtn.textContent = 'Add New Notice';
                        submitNoticeBtn.classList.remove('bg-green-600', 'hover:bg-green-700');
                        submitNoticeBtn.classList.add('bg-blue-600', 'hover:bg-blue-700');
                        cancelEditNoticeBtn.classList.add('hidden');
                    } catch (error) {
                        console.error("Error saving notice:", error);
                        showMessageBox("Error", "Failed to save notice. Please try again.");
                    }
                });
            }

            if (cancelEditNoticeBtn) {
                cancelEditNoticeBtn.addEventListener('click', () => {
                    noticeForm.reset();
                    noticeIdInput.value = '';
                    submitNoticeBtn.textContent = 'Add New Notice';
                    submitNoticeBtn.classList.remove('bg-green-600', 'hover:bg-green-700');
                    submitNoticeBtn.classList.add('bg-blue-600', 'hover:bg-blue-700');
                    cancelEditNoticeBtn.classList.add('hidden');
                });
            }

            async function deleteNotice(id) {
                if (!db) {
                    showMessageBox("Error", "Notice board system unavailable (Firebase not initialized).");
                    return;
                }
                try {
                    const noticeDocRef = doc(db, `artifacts/${appId}/public/data/notices`, id);
                    await deleteDoc(noticeDocRef);
                    showMessageBox("Success", "Notice deleted successfully!");
                } catch (error) {
                    console.error("Error deleting notice:", error);
                    showMessageBox("Error", "Failed to delete notice. Please try again.");
                }
            }

            // Notice Board Display (Student Side)
            let unsubscribeStudentNotices = null;

            function setupStudentNoticesListener() {
                if (!db || unsubscribeStudentNotices) return;

                const noticesCollectionRef = collection(db, `artifacts/${appId}/public/data/notices`);
                const q = query(noticesCollectionRef); // Removed orderBy as per instructions, will sort in memory

                unsubscribeStudentNotices = onSnapshot(q, (snapshot) => {
                    const notices = [];
                    snapshot.forEach(doc => {
                        notices.push({ id: doc.id, ...doc.data() });
                    });

                    // Sort notices by timestamp (most recent first)
                    notices.sort((a, b) => {
                        const dateA = a.timestamp ? a.timestamp.toDate() : new Date(0);
                        const dateB = b.timestamp ? b.timestamp.toDate() : new Date(0);
                        return dateB - dateA;
                    });

                    renderStudentNotices(notices);
                }, (error) => {
                    console.error("Error listening to student notices:", error);
                    studentNoticesDisplay.innerHTML = '<p class="text-red-600 text-center">Error loading notices.</p>';
                    noStudentNoticesMsg.classList.remove('hidden');
                });
            }

            function renderStudentNotices(notices) {
                if (notices.length === 0) {
                    studentNoticesDisplay.innerHTML = '<p class="text-gray-600 text-center" id="noStudentNotices">No notices available.</p>';
                    noStudentNoticesMsg.classList.remove('hidden');
                } else {
                    noStudentNoticesMsg.classList.add('hidden');
                    studentNoticesDisplay.innerHTML = '';
                    notices.forEach(notice => {
                        const noticeElement = document.createElement('div');
                        noticeElement.classList.add('bg-gray-50', 'p-4', 'rounded-lg', 'shadow-sm', 'border-l-4', 'border-blue-300');
                        
                        const date = notice.timestamp ? new Date(notice.timestamp.toDate()).toLocaleString() : 'N/A';

                        noticeElement.innerHTML = `
                            <h4 class="text-xl font-semibold text-gray-800 mb-1">${notice.title}</h4>
                            <p class="text-gray-700 leading-relaxed">${notice.content}</p>
                            <p class="text-xs text-gray-500 mt-2">Posted: ${date}</p>
                        `;
                        studentNoticesDisplay.appendChild(noticeElement);
                    });
                }
            }


            // --- MEMORY VERSE MANAGEMENT (ADMIN SIDE) ---
            let unsubscribeMemoryVerses = null;

            function setupAdminMemoryVersesListener() {
                if (!db || unsubscribeMemoryVerses) return;

                const memoryVersesCollectionRef = collection(db, `artifacts/${appId}/public/data/memoryVerses`);
                const q = query(memoryVersesCollectionRef);

                unsubscribeMemoryVerses = onSnapshot(q, (snapshot) => {
                    const verses = [];
                    snapshot.forEach(doc => {
                        verses.push({ id: doc.id, ...doc.data() });
                    });

                    // Sort verses by 'order' if it exists, otherwise by timestamp or just keep default order
                    verses.sort((a, b) => {
                        if (a.order !== undefined && b.order !== undefined) {
                            return a.order - b.order;
                        }
                        const dateA = a.timestamp ? a.timestamp.toDate() : new Date(0);
                        const dateB = b.timestamp ? b.timestamp.toDate() : new Date(0);
                        return dateB - dateA;
                    });

                    renderAdminMemoryVerses(verses);
                }, (error) => {
                    console.error("Error listening to memory verses:", error);
                    adminMemoryVersesList.innerHTML = '<p class="text-red-600 text-center">Error loading memory verses.</p>';
                    noAdminMemoryVersesMsg.classList.remove('hidden');
                });
            }

            function renderAdminMemoryVerses(verses) {
                if (verses.length === 0) {
                    adminMemoryVersesList.innerHTML = '<p class="text-gray-600 text-center" id="noAdminMemoryVerses">No memory verses currently posted.</p>';
                    noAdminMemoryVersesMsg.classList.remove('hidden');
                } else {
                    noAdminMemoryVersesMsg.classList.add('hidden');
                    adminMemoryVersesList.innerHTML = '';
                    verses.forEach(verse => {
                        const verseElement = document.createElement('div');
                        verseElement.classList.add('bg-gray-50', 'p-4', 'rounded-lg', 'shadow-sm', 'border-l-4', 'border-yellow-400', 'flex', 'flex-col', 'md:flex-row', 'md:items-center', 'md:justify-between', 'space-y-2', 'md:space-y-0');
                        
                        const timestamp = verse.timestamp ? new Date(verse.timestamp.toDate()).toLocaleString() : 'N/A';

                        verseElement.innerHTML = `
                            <div>
                                <p class="text-lg font-semibold text-gray-800">${verse.verseText}</p>
                                <p class="text-sm text-gray-700 mt-1">${verse.reference}</p>
                                <p class="text-xs text-gray-500 mt-1">Added: ${timestamp}</p>
                            </div>
                            <div class="flex space-x-2 mt-2 md:mt-0">
                                <button class="edit-verse-btn bg-yellow-500 text-white font-semibold py-1 px-3 rounded-full text-sm shadow-md hover:bg-yellow-600 transition-all-ease" data-id="${verse.id}" data-text="${encodeURIComponent(verse.verseText)}" data-reference="${encodeURIComponent(verse.reference)}">Edit</button>
                                <button class="delete-verse-btn bg-red-500 text-white font-semibold py-1 px-3 rounded-full text-sm shadow-md hover:bg-red-600 transition-all-ease" data-id="${verse.id}">Delete</button>
                            </div>
                        `;
                        adminMemoryVersesList.appendChild(verseElement);
                    });

                    adminMemoryVersesList.querySelectorAll('.edit-verse-btn').forEach(button => {
                        button.addEventListener('click', (e) => {
                            const id = e.target.dataset.id;
                            const text = decodeURIComponent(e.target.dataset.text);
                            const reference = decodeURIComponent(e.target.dataset.reference);
                            
                            memoryVerseIdInput.value = id;
                            memoryVerseTextInput.value = text;
                            memoryVerseReferenceInput.value = reference;
                            submitMemoryVerseBtn.textContent = 'Update Verse';
                            submitMemoryVerseBtn.classList.remove('bg-blue-600', 'hover:bg-blue-700');
                            submitMemoryVerseBtn.classList.add('bg-green-600', 'hover:bg-green-700');
                            cancelEditMemoryVerseBtn.classList.remove('hidden');
                        });
                    });

                    adminMemoryVersesList.querySelectorAll('.delete-verse-btn').forEach(button => {
                        button.addEventListener('click', async (e) => {
                            const id = e.target.dataset.id;
                            if (confirm("Are you sure you want to delete this memory verse?")) {
                                await deleteMemoryVerse(id);
                            }
                        });
                    });
                }
            }

            if (memoryVerseForm) {
                memoryVerseForm.addEventListener('submit', async (e) => {
                    e.preventDefault();
                    if (!db) {
                        showMessageBox("Error", "Memory verse system unavailable (Firebase not initialized).");
                        return;
                    }

                    const id = memoryVerseIdInput.value;
                    const verseText = memoryVerseTextInput.value.trim();
                    const reference = memoryVerseReferenceInput.value.trim();

                    if (!verseText || !reference) {
                        showMessageBox("Validation Error", "Please fill in both verse text and reference.");
                        return;
                    }

                    const memoryVersesCollectionRef = collection(db, `artifacts/${appId}/public/data/memoryVerses`);

                    try {
                        if (id) { // Editing existing verse
                            const verseDocRef = doc(memoryVersesCollectionRef, id);
                            await updateDoc(verseDocRef, { verseText, reference, timestamp: serverTimestamp() });
                            showMessageBox("Success", "Memory verse updated successfully!");
                        } else { // Adding new verse
                            await addDoc(memoryVersesCollectionRef, { verseText, reference, timestamp: serverTimestamp() });
                            showMessageBox("Success", "Memory verse added successfully!");
                        }
                        memoryVerseForm.reset();
                        memoryVerseIdInput.value = '';
                        submitMemoryVerseBtn.textContent = 'Add New Verse';
                        submitMemoryVerseBtn.classList.remove('bg-green-600', 'hover:bg-green-700');
                        submitMemoryVerseBtn.classList.add('bg-blue-600', 'hover:bg-blue-700');
                        cancelEditMemoryVerseBtn.classList.add('hidden');
                    } catch (error) {
                        console.error("Error saving memory verse:", error);
                        showMessageBox("Error", "Failed to save memory verse. Please try again.");
                    }
                });
            }

            if (cancelEditMemoryVerseBtn) {
                cancelEditMemoryVerseBtn.addEventListener('click', () => {
                    memoryVerseForm.reset();
                    memoryVerseIdInput.value = '';
                    submitMemoryVerseBtn.textContent = 'Add New Verse';
                    submitMemoryVerseBtn.classList.remove('bg-green-600', 'hover:bg-green-700');
                    submitMemoryVerseBtn.classList.add('bg-blue-600', 'hover:bg-blue-700');
                    cancelEditMemoryVerseBtn.classList.add('hidden');
                });
            }

            async function deleteMemoryVerse(id) {
                if (!db) {
                    showMessageBox("Error", "Memory verse system unavailable (Firebase not initialized).");
                    return;
                }
                try {
                    const verseDocRef = doc(db, `artifacts/${appId}/public/data/memoryVerses`, id);
                    await deleteDoc(verseDocRef);
                    showMessageBox("Success", "Memory verse deleted successfully!");
                } catch (error) {
                    console.error("Error deleting memory verse:", error);
                    showMessageBox("Error", "Failed to delete memory verse. Please try again.");
                }
            }


            // --- MEMORY VERSE DISPLAY (STUDENT SIDE) ---
            let unsubscribeStudentMemoryVerses = null;

            function setupStudentMemoryVersesListener() {
                if (!db || unsubscribeStudentMemoryVerses) return;

                const memoryVersesCollectionRef = collection(db, `artifacts/${appId}/public/data/memoryVerses`);
                const q = query(memoryVersesCollectionRef);

                unsubscribeStudentMemoryVerses = onSnapshot(q, (snapshot) => {
                    const verses = [];
                    snapshot.forEach(doc => {
                        verses.push({ id: doc.id, ...doc.data() });
                    });

                    verses.sort((a, b) => {
                        if (a.order !== undefined && b.order !== undefined) {
                            return a.order - b.order;
                        }
                        const dateA = a.timestamp ? a.timestamp.toDate() : new Date(0);
                        const dateB = b.timestamp ? b.timestamp.toDate() : new Date(0);
                        return dateB - dateA;
                    });

                    renderStudentMemoryVerses(verses);
                }, (error) => {
                    console.error("Error listening to student memory verses:", error);
                    memoryVersesList.innerHTML = '<p class="text-red-600 text-center">Error loading memory verses.</p>';
                    noStudentMemoryVerses.classList.remove('hidden');
                });
            }

            function renderStudentMemoryVerses(verses) {
                memoryVersesList.innerHTML = ''; // Clear previous content
                if (verses.length === 0) {
                    noStudentMemoryVerses.classList.remove('hidden');
                    readMoreVersesBtn.classList.add('hidden');
                } else {
                    noStudentMemoryVerses.classList.add('hidden');
                    const initialDisplayCount = 2; // Show first two verses
                    let allVersesVisible = false; // Track if all verses are currently shown

                    // Initial rendering
                    for (let i = 0; i < Math.min(verses.length, initialDisplayCount); i++) {
                        appendVerseToStudentList(verses[i]);
                    }

                    if (verses.length > initialDisplayCount) {
                        readMoreVersesBtn.classList.remove('hidden');
                        readMoreVersesBtn.textContent = 'Read More Verses';
                    } else {
                        readMoreVersesBtn.classList.add('hidden');
                    }

                    // Handle "Read More/Less" functionality
                    readMoreVersesBtn.onclick = function() {
                        if (!allVersesVisible) {
                            // Show remaining verses
                            for (let i = initialDisplayCount; i < verses.length; i++) {
                                appendVerseToStudentList(verses[i]);
                            }
                            readMoreVersesBtn.textContent = 'Read Less Verses';
                            allVersesVisible = true;
                        } else {
                            // Hide extra verses, keep only initialDisplayCount
                            memoryVersesList.innerHTML = ''; // Clear all
                            for (let i = 0; i < initialDisplayCount; i++) {
                                appendVerseToStudentList(verses[i]); // Re-add initial ones
                            }
                            readMoreVersesBtn.textContent = 'Read More Verses';
                            allVersesVisible = false;
                        }
                    };
                }
            }

            function appendVerseToStudentList(verse) {
                const li = document.createElement('li');
                li.innerHTML = `
                    "${verse.verseText}"
                    <span class="block text-gray-600 text-sm mt-1">${verse.reference}</span>
                    <button class="llm-explain-verse-btn mt-2 bg-blue-500 text-white text-sm font-semibold py-1 px-3 rounded-full shadow-md hover:bg-blue-600 transition-all-ease" data-verse="${encodeURIComponent(`"${verse.verseText}" ${verse.reference}`)}">
                        ✨ Explain Verse
                    </button>
                    <div class="llm-response-section hidden"></div>
                `;
                memoryVersesList.appendChild(li);
            }


            // --- Gemini API Integration Functions ---

            // General function to call LLM (gemini-2.0-flash)
            async function callGeminiAPI(prompt, outputElement, loadingElement) {
                loadingElement.classList.remove('hidden');
                outputElement.classList.add('hidden');
                outputElement.innerHTML = ''; // Clear previous content

                let chatHistory = [];
                chatHistory.push({ role: "user", parts: [{ text: prompt }] });
                const payload = { contents: chatHistory };
                const apiKey = ""; // Canvas will provide this at runtime.

                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    const result = await response.json();
                    
                    if (result.candidates && result.candidates.length > 0 &&
                        result.candidates[0].content && result.candidates[0].content.parts &&
                        result.candidates[0].content.parts.length > 0) {
                        const text = result.candidates[0].content.parts[0].text;
                        outputElement.innerHTML = text.replace(/\n/g, '<br>'); // Simple newline to <br> for display
                        outputElement.classList.remove('hidden');
                    } else {
                        outputElement.innerHTML = '<p class="text-red-500">Could not generate response. Please try again.</p>';
                        outputElement.classList.remove('hidden');
                        console.error('Gemini API response structure unexpected:', result);
                    }
                } catch (error) {
                    console.error('Error calling Gemini API:', error);
                    outputElement.innerHTML = '<p class="text-red-500">Error connecting to AI. Please check your network or try again.</p>';
                    outputElement.classList.remove('hidden');
                } finally {
                    loadingElement.classList.add('hidden');
                }
            }

            // Student Dashboard: Memory Verse Explainer (using event delegation for dynamic buttons)
            if (memoryVersesList) {
                memoryVersesList.addEventListener('click', async (e) => {
                    if (e.target.classList.contains('llm-explain-verse-btn')) {
                        const verse = decodeURIComponent(e.target.dataset.verse);
                        // Find the sibling .llm-response-section div
                        const responseContainer = e.target.nextElementSibling;
                        
                        // Toggle visibility if already open
                        if (responseContainer.classList.contains('show-llm-response')) {
                            responseContainer.classList.remove('show-llm-response');
                            responseContainer.classList.add('hidden');
                            e.target.textContent = '✨ Explain Verse';
                            return;
                        }

                        // Prepare for loading state
                        e.target.textContent = 'Generating...'; // Indicate loading on the button
                        responseContainer.classList.remove('hidden');
                        responseContainer.classList.add('show-llm-response');
                        responseContainer.innerHTML = `
                            <div class="llm-loading-indicator">
                                <div class="llm-loading-spinner"></div>
                                <span>Getting explanation...</span>
                            </div>
                        `;

                        const prompt = `Provide a simplified explanation, a brief context, and a short devotional thought for Sunday school children (ages 6-10) for the following Bible verse:\n\n"${verse}"\n\nFormat your response with clear headings for Explanation, Context, and Devotional Thought. Keep it concise and easy to understand.`;
                        
                        try {
                            let chatHistory = [];
                            chatHistory.push({ role: "user", parts: [{ text: prompt }] });
                            const payload = { contents: chatHistory };
                            const apiKey = ""; // Canvas will provide this at runtime.

                            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`;

                            const response = await fetch(apiUrl, {
                                method: 'POST',
                                headers: { 'Content-Type': 'application/json' },
                                body: JSON.stringify(payload)
                            });
                            const result = await response.json();

                            if (result.candidates && result.candidates.length > 0 &&
                                result.candidates[0].content && result.candidates[0].content.parts &&
                                result.candidates[0].content.parts.length > 0) {
                                const text = result.candidates[0].content.parts[0].text;
                                // Simple parsing for expected headings
                                const explanationMatch = text.match(/Explanation:\s*(.*?)(?:Context:|$)/s);
                                const contextMatch = text.match(/Context:\s*(.*?)(?:Devotional Thought:|$)/s);
                                const devotionalMatch = text.match(/Devotional Thought:\s*(.*)/s);

                                const explanation = explanationMatch ? explanationMatch[1].trim() : 'N/A';
                                const context = contextMatch ? contextMatch[1].trim() : 'N/A';
                                const devotional = devotionalMatch ? devotionalMatch[1].trim() : 'N/A';

                                responseContainer.innerHTML = `
                                    <h4>Explanation:</h4>
                                    <p>${explanation.replace(/\n/g, '<br>')}</p>
                                    <h4>Context:</h4>
                                    <p>${context.replace(/\n/g, '<br>')}</p>
                                    <h4>Devotional Thought:</h4>
                                    <p>${devotional.replace(/\n/g, '<br>')}</p>
                                `;
                                e.target.textContent = 'Hide Explanation';
                            } else {
                                responseContainer.innerHTML = '<p class="text-red-500">Could not get explanation. Try again.</p>';
                                e.target.textContent = '✨ Explain Verse';
                                console.error('Gemini API response structure unexpected:', result);
                            }
                        } catch (error) {
                            console.error('Error calling Gemini API for verse explanation:', error);
                            responseContainer.innerHTML = '<p class="text-red-500">Error fetching explanation. Please try again.</p>';
                            e.target.textContent = '✨ Explain Verse';
                        }
                    }
                });
            }


            // Admin Dashboard: Lesson Plan Idea Generator
            if (lessonIdeaForm) {
                lessonIdeaForm.addEventListener('submit', async (e) => {
                    e.preventDefault();
                    const topic = lessonTopicInput.value.trim();

                    if (!topic) {
                        showMessageBox("Input Required", "Please enter a lesson topic.");
                        return;
                    }

                    const prompt = `Generate a comprehensive Sunday school lesson plan outline for the topic "${topic}". Include sections for:
                    1.  **Objective:** What students should learn.
                    2.  **Key Verse(s):** Relevant Bible verses.
                    3.  **Opening Activity/Icebreaker:** An engaging start.
                    4.  **Bible Story/Teaching Points:** Main narrative or concepts.
                    5.  **Discussion Questions:** Questions to promote understanding and application.
                    6.  **Creative Activity/Craft:** Hands-on activity.
                    7.  **Prayer/Closing:** A concluding prayer or thought.
                    
                    Ensure the tone is appropriate for children (ages 6-12) and the ideas are practical for a Sunday school setting. Format the output clearly using bolding for headings and bullet points/paragraphs for content.`;
                    
                    await callGeminiAPI(prompt, lessonIdeasContent, lessonIdeasLoading);
                    lessonIdeasOutput.classList.remove('hidden'); // Ensure the output container is visible
                });
            }

            // NEW: Admin Memory Verse Recitation Tracking Functions
            async function populateRecitationCheckboxes(grade, checkboxesContainerElement, selectedDate) {
                const container = checkboxesContainerElement;
                if (!container) return;
                container.innerHTML = ''; // Clear existing checkboxes

                let existingRecitations = {};
                if (db) {
                    try {
                        const recitationDocRef = doc(db, `artifacts/${appId}/public/data/dailyMemoryVerseRecitations`, selectedDate);
                        const docSnap = await getDoc(recitationDocRef);
                        if (docSnap.exists()) {
                            existingRecitations = docSnap.data();
                        }
                    } catch (error) {
                        console.error("Error fetching existing recitations:", error);
                        showMessageBox("Error", "Could not load previous recitation records.");
                    }
                }

                studentData[grade].forEach(student => {
                    const username = student.name.toLowerCase().replace(/\s/g, '');
                    const hasRecited = existingRecitations[username] === true;

                    const label = document.createElement('label');
                    label.classList.add('flex', 'items-center', 'space-x-2');
                    label.innerHTML = `
                        <input type="checkbox" name="recitation" value="${username}" ${hasRecited ? 'checked' : ''} class="form-checkbox h-5 w-5 text-purple-600 rounded">
                        <span class="text-gray-800">${student.name}</span>
                    `;
                    container.appendChild(label);
                });
            }

            async function handleRecitationSubmission(event, grade) {
                event.preventDefault();
                if (!db) {
                    showMessageBox("Error", "Recitation tracking system unavailable (Firebase not initialized).");
                    return;
                }

                const selectedDate = recitationDateInput.value;
                if (!selectedDate) {
                    showMessageBox("Error", "Please select a date for recitation tracking.");
                    return;
                }

                const form = event.target;
                const checkboxes = form.querySelectorAll('input[name="recitation"]');
                const recitationUpdates = {};

                checkboxes.forEach(checkbox => {
                    recitationUpdates[checkbox.value] = checkbox.checked;
                });

                const recitationDocRef = doc(db, `artifacts/${appId}/public/data/dailyMemoryVerseRecitations`, selectedDate);

                try {
                    await setDoc(recitationDocRef, recitationUpdates, { merge: true });
                    showMessageBox("Success", `Memory verse recitation marks recorded for ${grade} on ${selectedDate}!`);
                } catch (error) {
                    console.error("Error submitting recitation marks:", error);
                    showMessageBox("Error", "Failed to record recitation marks. Please try again.");
                }
            }

            // Event Listeners for Admin Recitation Tracking
            if (adminViewSubJuniorRecitationBtn) {
                adminViewSubJuniorRecitationBtn.addEventListener('click', function() {
                    adminSubJuniorRecitationContainer.classList.toggle('hidden');
                    if (!adminSubJuniorRecitationContainer.classList.contains('hidden')) {
                        populateRecitationCheckboxes('subJunior', subJuniorRecitationCheckboxes, recitationDateInput.value);
                        adminViewSubJuniorRecitationBtn.textContent = 'Hide Sub Junior Recitation';
                    } else {
                        adminViewSubJuniorRecitationBtn.textContent = 'View Sub Junior Recitation';
                    }
                });
            }
            if (adminSubJuniorRecitationForm) {
                adminSubJuniorRecitationForm.addEventListener('submit', (event) => handleRecitationSubmission(event, 'subJunior'));
            }

            if (adminViewJuniorRecitationBtn) {
                adminViewJuniorRecitationBtn.addEventListener('click', function() {
                    adminJuniorRecitationContainer.classList.toggle('hidden');
                    if (!adminJuniorRecitationContainer.classList.contains('hidden')) {
                        populateRecitationCheckboxes('junior', juniorRecitationCheckboxes, recitationDateInput.value);
                        adminViewJuniorRecitationBtn.textContent = 'Hide Junior Recitation';
                    } else {
                        adminViewJuniorRecitationBtn.textContent = 'View Junior Recitation';
                    }
                });
            }
            if (adminJuniorRecitationForm) {
                adminJuniorRecitationForm.addEventListener('submit', (event) => handleRecitationSubmission(event, 'junior'));
            }

            if (adminViewSeniorRecitationBtn) {
                adminViewSeniorRecitationBtn.addEventListener('click', function() {
                    adminSeniorRecitationContainer.classList.toggle('hidden');
                    if (!adminSeniorRecitationContainer.classList.contains('hidden')) {
                        populateRecitationCheckboxes('senior', seniorRecitationCheckboxes, recitationDateInput.value);
                        adminViewSeniorRecitationBtn.textContent = 'Hide Senior Recitation';
                    } else {
                        adminViewSeniorRecitationBtn.textContent = 'View Senior Recitation';
                    }
                });
            }
            if (adminSeniorRecitationForm) {
                adminSeniorRecitationForm.addEventListener('submit', (event) => handleRecitationSubmission(event, 'senior'));
            }


            // --- TEACHER DASHBOARD SPECIFIC FUNCTIONALITY ---

            // Helper to toggle visibility and populate table/form for teacher sections
            function toggleTeacherClassSection(grade, classDetailsDiv, tableBodyElement, attendanceFormElement, viewButton) {
                classDetailsDiv.classList.toggle('hidden');
                if (!classDetailsDiv.classList.contains('hidden')) {
                    // Populate table and attendance checkboxes for the specific grade
                    populateAttendanceCheckboxes(grade, tableBodyElement, attendanceFormElement.id, true); // true for isTeacher
                    viewButton.textContent = `Hide ${grade} Class Details`;
                } else {
                    viewButton.textContent = `View Students & Mark Attendance`;
                }
            }

            if (teacherViewSubJuniorStudentsBtn) {
                teacherViewSubJuniorStudentsBtn.addEventListener('click', () => {
                    toggleTeacherClassSection('subJunior', teacherSubJuniorClassDetails, teacherSubJuniorStudentsTableBody, teacherSubJuniorAttendanceForm, teacherViewSubJuniorStudentsBtn);
                });
            }
            if (teacherViewJuniorStudentsBtn) {
                teacherViewJuniorStudentsBtn.addEventListener('click', () => {
                    toggleTeacherClassSection('junior', teacherJuniorClassDetails, teacherJuniorStudentsTableBody, teacherJuniorAttendanceForm, teacherViewJuniorStudentsBtn);
                });
            }
            if (teacherViewSeniorStudentsBtn) {
                teacherViewSeniorStudentsBtn.addEventListener('click', () => {
                    toggleTeacherClassSection('senior', teacherSeniorClassDetails, teacherSeniorStudentsTableBody, teacherSeniorAttendanceForm, teacherViewSeniorStudentsBtn); // Fixed typo: teacherViewSeniorSeniorStudentsBtn
                });
            }
            
            // Teacher - Notice Board Display (same as student side, but in teacher section)
            let unsubscribeTeacherNotices = null;

            function setupTeacherNoticesListener() {
                if (!db || unsubscribeTeacherNotices) return;

                const noticesCollectionRef = collection(db, `artifacts/${appId}/public/data/notices`);
                const q = query(noticesCollectionRef);

                unsubscribeTeacherNotices = onSnapshot(q, (snapshot) => {
                    const notices = [];
                    snapshot.forEach(doc => {
                        notices.push({ id: doc.id, ...doc.data() });
                    });

                    notices.sort((a, b) => {
                        const dateA = a.timestamp ? a.timestamp.toDate() : new Date(0);
                        const dateB = b.timestamp ? b.timestamp.toDate() : new Date(0);
                        return dateB - dateA;
                    });

                    renderTeacherNotices(notices);
                }, (error) => {
                    console.error("Error listening to teacher notices:", error);
                    teacherNoticesDisplay.innerHTML = '<p class="text-red-600 text-center">Error loading notices.</p>';
                    noTeacherNotices.classList.remove('hidden');
                });
            }

            function renderTeacherNotices(notices) {
                if (notices.length === 0) {
                    teacherNoticesDisplay.innerHTML = '<p class="text-gray-600 text-center" id="noTeacherNotices">No notices available.</p>';
                    noTeacherNotices.classList.remove('hidden');
                } else {
                    noTeacherNotices.classList.add('hidden');
                    teacherNoticesDisplay.innerHTML = '';
                    notices.forEach(notice => {
                        const noticeElement = document.createElement('div');
                        noticeElement.classList.add('bg-gray-50', 'p-4', 'rounded-lg', 'shadow-sm', 'border-l-4', 'border-green-300'); // Green border for teacher notices
                        
                        const date = notice.timestamp ? new Date(notice.timestamp.toDate()).toLocaleString() : 'N/A';

                        noticeElement.innerHTML = `
                            <h4 class="text-xl font-semibold text-gray-800 mb-1">${notice.title}</h4>
                            <p class="text-gray-700 leading-relaxed">${notice.content}</p>
                            <p class="text-xs text-gray-500 mt-2">Posted: ${date}</p>
                        `;
                        teacherNoticesDisplay.appendChild(noticeElement);
                    });
                }
            }


            // Teacher - Leave Applications View (Read-only for teachers, can approve/disapprove)
            async function fetchAndDisplayTeacherLeaveApplications() {
                if (!db) {
                    teacherPendingLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center text-red-500">Leave application management unavailable (Firebase not initialized).</p>';
                    return;
                }

                teacherPendingLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center">Loading student applications...</p>';
                const publicLeaveAppInboxRef = collection(db, `artifacts/${appId}/public/data/leaveApplicationsInbox`);
                
                try {
                    // Fetch all applications, teachers might oversee multiple grades
                    // For a more complex setup, you'd filter by grade assigned to the teacher
                    const q = query(publicLeaveAppInboxRef); 
                    const querySnapshot = await getDocs(q);

                    if (querySnapshot.empty) {
                        teacherPendingLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center" id="noTeacherPendingApplications">No student leave applications.</p>';
                        noTeacherPendingApplicationsMsg.classList.remove('hidden');
                    } else {
                        noTeacherPendingApplicationsMsg.classList.add('hidden');
                        teacherPendingLeaveApplicationsDiv.innerHTML = ''; // Clear loading message

                        // Filter and sort applications in memory
                        const pendingApplications = [];
                        querySnapshot.forEach(appDoc => {
                            const appData = appDoc.data();
                            if (appData.status === "Pending") { // Only show "Pending" applications
                                pendingApplications.push({ id: appDoc.id, ...appData });
                            }
                        });

                        pendingApplications.sort((a, b) => {
                            const dateA = a.submissionTimestamp ? a.submissionTimestamp.toDate() : new Date(a.submissionDate);
                            const dateB = b.submissionTimestamp ? b.submissionTimestamp.toDate() : new Date(b.submissionDate);
                            return dateB - dateA;
                        });

                        if (pendingApplications.length === 0) {
                            teacherPendingLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center" id="noTeacherPendingApplications">No pending student leave applications.</p>';
                            noTeacherPendingApplicationsMsg.classList.remove('hidden');
                        } else {
                             pendingApplications.forEach(app => {
                                const appElement = document.createElement('div');
                                appElement.classList.add('bg-green-50', 'p-4', 'rounded-lg', 'shadow-sm', 'border-l-4', 'border-green-500', 'flex', 'flex-col', 'md:flex-row', 'md:items-center', 'md:justify-between', 'space-y-3', 'md:space-y-0');
                                
                                const studentInfo = app.studentFullName || app.studentUsername || "Unknown Student";

                                appElement.innerHTML = `
                                    <div>
                                        <p class="text-md font-semibold text-green-800 mb-1">Student: ${studentInfo}</p>
                                        <p class="text-sm text-gray-700 mb-1">Reason: ${app.reason}</p>
                                        <p class="text-xs text-gray-600">From: ${app.startDate} To: ${app.endDate}</p>
                                        <p class="text-xs text-gray-500">Submitted: ${new Date(app.submissionDate).toLocaleString()}</p>
                                    </div>
                                    <div class="flex space-x-2">
                                        <button class="approve-btn bg-green-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-green-600 transition-all-ease" data-public-doc-id="${app.id}" data-student-id="${app.studentId}" data-private-doc-id="${app.privateDocId}">Approve</button>
                                        <button class="disapprove-btn bg-red-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-red-600 transition-all-ease" data-public-doc-id="${app.id}" data-student-id="${app.studentId}" data-private-doc-id="${app.privateDocId}">Disapprove</button>
                                    </div>
                                `;
                                teacherPendingLeaveApplicationsDiv.appendChild(appElement);
                            });

                            // Attach event listeners to the new buttons
                            teacherPendingLeaveApplicationsDiv.querySelectorAll('.approve-btn').forEach(button => {
                                button.addEventListener('click', handleLeaveAction); // Re-use handleLeaveAction
                            });
                            teacherPendingLeaveApplicationsDiv.querySelectorAll('.disapprove-btn').forEach(button => {
                                button.addEventListener('click', handleLeaveAction); // Re-use handleLeaveAction
                            });
                        }
                    }
                } catch (error) {
                    console.error("Error fetching teacher leave applications:", error);
                    teacherPendingLeaveApplicationsDiv.innerHTML = '<p class="text-gray-600 text-center text-red-500">Failed to load student leave applications.</p>';
                }
            }

            // Function to handle "Mark All" buttons
            function handleMarkAll(grade, isPresent) {
                let containerId;
                if (currentUsername === ADMIN_USERNAME) {
                    containerId = `admin${grade.charAt(0).toUpperCase() + grade.slice(1)}AttendanceFormContainer`;
                } else if (currentUsername === TEACHER_USERNAME) {
                    containerId = `teacher${grade.charAt(0).toUpperCase() + grade.slice(1)}ClassDetails`;
                } else {
                    return; // Should not happen for these buttons
                }

                const formContainer = document.getElementById(containerId);
                if (!formContainer) return;

                // Find all attendance checkboxes within this specific form container
                const checkboxes = formContainer.querySelectorAll('input[name="attendance"]');
                checkboxes.forEach(checkbox => {
                    checkbox.checked = isPresent;
                });
            }

            // Add event listeners using delegation to catch clicks on "Mark All" buttons
            document.addEventListener('click', function(event) {
                if (event.target.classList.contains('mark-all-present-btn')) {
                    const grade = event.target.dataset.grade;
                    handleMarkAll(grade, true);
                } else if (event.target.classList.contains('mark-all-absent-btn')) {
                    const grade = event.target.dataset.grade;
                    handleMarkAll(grade, false);
                }
            });

            // --- DOWNLOADS CENTRE MANAGEMENT (ADMIN SIDE) ---
            let unsubscribeDownloads = null;

            function setupAdminDownloadsListener() {
                if (!db || unsubscribeDownloads) return;

                const downloadsCollectionRef = collection(db, `artifacts/${appId}/public/data/downloads`);
                const q = query(downloadsCollectionRef);

                unsubscribeDownloads = onSnapshot(q, (snapshot) => {
                    const downloads = [];
                    snapshot.forEach(doc => {
                        downloads.push({ id: doc.id, ...doc.data() });
                    });

                    // Sort downloads by timestamp (most recent first)
                    downloads.sort((a, b) => {
                        const dateA = a.timestamp ? a.timestamp.toDate() : new Date(0);
                        const dateB = b.timestamp ? b.timestamp.toDate() : new Date(0);
                        return dateB - dateA;
                    });

                    renderAdminDownloads(downloads);
                }, (error) => {
                    console.error("Error listening to downloads:", error);
                    adminDownloadsList.innerHTML = '<p class="text-red-600 text-center">Error loading downloads.</p>';
                    noAdminDownloadsMsg.classList.remove('hidden');
                });
            }

            function renderAdminDownloads(downloads) {
                if (downloads.length === 0) {
                    adminDownloadsList.innerHTML = '<p class="text-gray-600 text-center" id="noAdminDownloads">No downloadable files currently posted.</p>';
                    noAdminDownloadsMsg.classList.remove('hidden');
                } else {
                    noAdminDownloadsMsg.classList.add('hidden');
                    adminDownloadsList.innerHTML = '';
                    downloads.forEach(download => {
                        const downloadElement = document.createElement('div');
                        downloadElement.classList.add('bg-gray-50', 'p-4', 'rounded-lg', 'shadow-sm', 'border-l-4', 'border-purple-400', 'flex', 'flex-col', 'md:flex-row', 'md:items-center', 'md:justify-between', 'space-y-2', 'md:space-y-0');
                        
                        const timestamp = download.timestamp ? new Date(download.timestamp.toDate()).toLocaleString() : 'N/A';
                        const descriptionHtml = download.description ? `<p class="text-gray-600 text-sm mt-1">${download.description}</p>` : '';
                        const categoryHtml = download.category ? `<p class="text-xs text-gray-500 mt-1">Category: ${download.category}</p>` : '';

                        downloadElement.innerHTML = `
                            <div>
                                <h4 class="text-lg font-semibold text-gray-800"><a href="${download.url}" target="_blank" class="text-blue-600 hover:underline">${download.title}</a></h4>
                                ${descriptionHtml}
                                ${categoryHtml}
                                <p class="text-xs text-gray-500 mt-1">Added: ${timestamp}</p>
                            </div>
                            <div class="flex space-x-2 mt-2 md:mt-0">
                                <button class="edit-download-btn bg-yellow-500 text-white font-semibold py-1 px-3 rounded-full text-sm shadow-md hover:bg-yellow-600 transition-all-ease" 
                                    data-id="${download.id}" 
                                    data-title="${encodeURIComponent(download.title)}" 
                                    data-description="${encodeURIComponent(download.description || '')}"
                                    data-url="${encodeURIComponent(download.url)}"
                                    data-category="${encodeURIComponent(download.category || '')}">Edit</button>
                                <button class="delete-download-btn bg-red-500 text-white font-semibold py-1 px-3 rounded-full text-sm shadow-md hover:bg-red-600 transition-all-ease" data-id="${download.id}">Delete</button>
                            </div>
                        `;
                        adminDownloadsList.appendChild(downloadElement);
                    });

                    adminDownloadsList.querySelectorAll('.edit-download-btn').forEach(button => {
                        button.addEventListener('click', (e) => {
                            const id = e.target.dataset.id;
                            const title = decodeURIComponent(e.target.dataset.title);
                            const description = decodeURIComponent(e.target.dataset.description);
                            const url = decodeURIComponent(e.target.dataset.url);
                            const category = decodeURIComponent(e.target.dataset.category);
                            
                            downloadIdInput.value = id;
                            downloadTitleInput.value = title;
                            downloadDescriptionInput.value = description;
                            downloadUrlInput.value = url;
                            downloadCategoryInput.value = category;

                            submitDownloadBtn.textContent = 'Update Download';
                            submitDownloadBtn.classList.remove('bg-blue-600', 'hover:bg-blue-700');
                            submitDownloadBtn.classList.add('bg-green-600', 'hover:bg-green-700');
                            cancelEditDownloadBtn.classList.remove('hidden');
                        });
                    });

                    adminDownloadsList.querySelectorAll('.delete-download-btn').forEach(button => {
                        button.addEventListener('click', async (e) => {
                            const id = e.target.dataset.id;
                            if (confirm("Are you sure you want to delete this downloadable file?")) {
                                await deleteDownload(id);
                            }
                        });
                    });
                }
            }

            if (downloadForm) {
                downloadForm.addEventListener('submit', async (e) => {
                    e.preventDefault();
                    if (!db) {
                        showMessageBox("Error", "Downloads system unavailable (Firebase not initialized).");
                        return;
                    }

                    const id = downloadIdInput.value;
                    const title = downloadTitleInput.value.trim();
                    const description = downloadDescriptionInput.value.trim();
                    const url = downloadUrlInput.value.trim();
                    const category = downloadCategoryInput.value.trim();

                    if (!title || !url) {
                        showMessageBox("Validation Error", "Please fill in both title and file URL.");
                        return;
                    }
                    if (!url.startsWith('http://') && !url.startsWith('https://')) {
                        showMessageBox("Validation Error", "Please enter a valid URL (must start with http:// or https://).");
                        return;
                    }


                    const downloadsCollectionRef = collection(db, `artifacts/${appId}/public/data/downloads`);

                    try {
                        if (id) { // Editing existing download
                            const downloadDocRef = doc(downloadsCollectionRef, id);
                            await updateDoc(downloadDocRef, { title, description, url, category, timestamp: serverTimestamp() });
                            showMessageBox("Success", "Download updated successfully!");
                        } else { // Adding new download
                            await addDoc(downloadsCollectionRef, { title, description, url, category, timestamp: serverTimestamp() });
                            showMessageBox("Success", "Download added successfully!");
                        }
                        downloadForm.reset();
                        downloadIdInput.value = '';
                        submitDownloadBtn.textContent = 'Add New Download';
                        submitDownloadBtn.classList.remove('bg-green-600', 'hover:bg-green-700');
                        submitDownloadBtn.classList.add('bg-blue-600', 'hover:bg-blue-700');
                        cancelEditDownloadBtn.classList.add('hidden');
                    } catch (error) {
                        console.error("Error saving download:", error);
                        showMessageBox("Error", "Failed to save download. Please try again.");
                    }
                });
            }

            if (cancelEditDownloadBtn) {
                cancelEditDownloadBtn.addEventListener('click', () => {
                    downloadForm.reset();
                    downloadIdInput.value = '';
                    submitDownloadBtn.textContent = 'Add New Download';
                    submitDownloadBtn.classList.remove('bg-green-600', 'hover:bg-green-700');
                    submitDownloadBtn.classList.add('bg-blue-600', 'hover:bg-blue-700');
                    cancelEditDownloadBtn.classList.add('hidden');
                });
            }

            async function deleteDownload(id) {
                if (!db) {
                    showMessageBox("Error", "Downloads system unavailable (Firebase not initialized).");
                    return;
                }
                try {
                    const downloadDocRef = doc(db, `artifacts/${appId}/public/data/downloads`, id);
                    await deleteDoc(downloadDocRef);
                    showMessageBox("Success", "Download deleted successfully!");
                } catch (error) {
                    console.error("Error deleting download:", error);
                    showMessageBox("Error", "Failed to delete download. Please try again.");
                }
            }

            // --- DOWNLOADS CENTRE DISPLAY (USER SIDE) ---
            let unsubscribeUserDownloads = null;

            function setupUserDownloadsListener() {
                if (!db || unsubscribeUserDownloads) return;

                const downloadsCollectionRef = collection(db, `artifacts/${appId}/public/data/downloads`);
                const q = query(downloadsCollectionRef);

                unsubscribeUserDownloads = onSnapshot(q, (snapshot) => {
                    const downloads = [];
                    snapshot.forEach(doc => {
                        downloads.push({ id: doc.id, ...doc.data() });
                    });

                    downloads.sort((a, b) => {
                        const dateA = a.timestamp ? a.timestamp.toDate() : new Date(0);
                        const dateB = b.timestamp ? b.timestamp.toDate() : new Date(0);
                        return dateB - dateA;
                    });

                    renderUserDownloads(downloads);
                }, (error) => {
                    console.error("Error listening to user downloads:", error);
                    userDownloadsList.innerHTML = '<p class="text-red-600 text-center">Error loading downloads.</p>';
                    noUserDownloadsMsg.classList.remove('hidden');
                });
            }

            function renderUserDownloads(downloads) {
                userDownloadsList.innerHTML = ''; // Clear previous content
                if (downloads.length === 0) {
                    noUserDownloadsMsg.classList.remove('hidden');
                } else {
                    noUserDownloadsMsg.classList.add('hidden');
                    downloads.forEach(download => {
                        const li = document.createElement('li');
                        li.innerHTML = `
                            <a href="${download.url}" target="_blank" class="text-blue-600 hover:underline font-medium">${download.title}</a>
                            ${download.description ? `<p class="text-gray-700 text-sm ml-4">${download.description}</p>` : ''}
                            ${download.category ? `<p class="text-gray-500 text-xs ml-4">Category: ${download.category}</p>` : ''}
                        `;
                        userDownloadsList.appendChild(li);
                    });
                }
            }

            // --- ATTENDANCE NOTIFICATIONS (ADMIN SIDE) ---
            let unsubscribeAttendanceNotifications = null;

            function setupAdminAttendanceNotificationsListener() {
                if (!db || unsubscribeAttendanceNotifications) return;

                const notificationsCollectionRef = collection(db, `artifacts/${appId}/public/data/attendanceNotifications`);
                const q = query(notificationsCollectionRef, where("status", "==", "Pending")); // Listen only for pending notifications

                unsubscribeAttendanceNotifications = onSnapshot(q, (snapshot) => {
                    const notifications = [];
                    snapshot.forEach(doc => {
                        notifications.push({ id: doc.id, ...doc.data() });
                    });

                    // Sort notifications by submission timestamp (most recent first)
                    notifications.sort((a, b) => {
                        const dateA = a.submissionTimestamp ? a.submissionTimestamp.toDate() : new Date(0);
                        const dateB = b.submissionTimestamp ? b.submissionTimestamp.toDate() : new Date(0); // Fixed typo: b.timestamp
                        return dateB - dateA;
                    });

                    renderAdminAttendanceNotifications(notifications);
                }, (error) => {
                    console.error("Error listening to attendance notifications:", error);
                    attendanceNotificationsList.innerHTML = '<p class="text-red-600 text-center">Error loading attendance notifications.</p>';
                    noAttendanceNotificationsMsg.classList.remove('hidden');
                });
            }

            function renderAdminAttendanceNotifications(notifications) {
                if (notifications.length === 0) {
                    attendanceNotificationsList.innerHTML = '<p class="text-gray-600 text-center" id="noAttendanceNotifications">No pending attendance notifications.</p>';
                    noAttendanceNotificationsMsg.classList.remove('hidden');
                } else {
                    noAttendanceNotificationsMsg.classList.add('hidden');
                    attendanceNotificationsList.innerHTML = ''; // Clear existing notifications
                    notifications.forEach(notification => {
                        const notificationElement = document.createElement('div');
                        notificationElement.classList.add('bg-blue-50', 'p-4', 'rounded-lg', 'shadow-sm', 'border-l-4', 'border-blue-500', 'flex', 'flex-col', 'md:flex-row', 'md:items-center', 'md:justify-between', 'space-y-3', 'md:space-y-0');
                        
                        const submittedDate = notification.submissionTimestamp ? new Date(notification.submissionTimestamp.toDate()).toLocaleString() : 'N/A';

                        notificationElement.innerHTML = `
                            <div>
                                <p class="text-md font-semibold text-blue-800 mb-1">Attendance for ${notification.grade.charAt(0).toUpperCase() + notification.grade.slice(1)} Class on ${notification.date}</p>
                                <p class="text-sm text-gray-700 mb-1">Submitted by: ${notification.submittedBy}</p>
                                <p class="text-xs text-gray-500">Submitted: ${submittedDate}</p>
                            </div>
                            <div class="flex space-x-2">
                                <button class="approve-attendance-btn bg-green-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-green-600 transition-all-ease" data-notification-id="${notification.id}">Approve</button>
                                <button class="disapprove-attendance-btn bg-red-500 text-white font-semibold py-2 px-4 rounded-full shadow-md hover:bg-red-600 transition-all-ease" data-notification-id="${notification.id}">Disapprove</button>
                            </div>
                        `;
                        attendanceNotificationsList.appendChild(notificationElement);
                    });

                    // Attach event listeners to the new buttons
                    attendanceNotificationsList.querySelectorAll('.approve-attendance-btn').forEach(button => {
                        button.addEventListener('click', (e) => handleAttendanceNotificationAction(e.target.dataset.notificationId, "Approved"));
                    });
                    attendanceNotificationsList.querySelectorAll('.disapprove-attendance-btn').forEach(button => {
                        button.addEventListener('click', (e) => handleAttendanceNotificationAction(e.target.dataset.notificationId, "Disapproved"));
                    });
                }
            }

            async function handleAttendanceNotificationAction(notificationId, action) {
                if (!db) {
                    showMessageBox("Error", "Database not connected. Cannot perform action.");
                    return;
                }

                const notificationDocRef = doc(db, `artifacts/${appId}/public/data/attendanceNotifications`, notificationId);

                try {
                    await updateDoc(notificationDocRef, { status: action });
                    showMessageBox("Success", `Attendance submission ${action.toLowerCase()}!`);
                } catch (error) {
                    console.error(`Error ${action.toLowerCase()} attendance notification:`, error);
                    showMessageBox("Error", `Failed to ${action.toLowerCase()} attendance notification. Please try again.`);
                }
            }

        });
    </script>

</body>
</html>
