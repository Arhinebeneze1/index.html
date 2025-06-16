<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Koffan Maths Education Platform</title>
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet" />
<style>
  /* Reset and base */
  *, *::before, *::after {
    box-sizing: border-box;
  }
  body {
    margin: 0; padding: 0;
    font-family: 'Inter', sans-serif;
    background: #ffffff;
    color: #374151;
    line-height: 1.5;
    font-size: 16px;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    user-select: text;
  }
  a {
    color: #3b82f6;
    text-decoration: none;
  }
  a:hover, a:focus {
    text-decoration: underline;
  }

  /* Layout containers */
  #app {
    display: grid;
    grid-template-areas:
      "header header header"
      "sidebar main right";
    grid-template-columns: 300px 1fr 320px;
    grid-template-rows: 60px 1fr;
    height: 100vh;
    overflow: hidden;
  }

  /* Responsive grid */
  @media (max-width: 1024px) {
    #app {
      grid-template-columns: 250px 1fr;
      grid-template-areas:
        "header header"
        "sidebar main"
        "sidebar right";
      grid-template-rows: 60px 1fr 1fr;
      height: 100vh;
    }
  }
  @media (max-width: 640px) {
    #app {
      display: flex;
      flex-direction: column;
      height: 100vh;
    }
  }

  /* Header */
  header {
    grid-area: header;
    background: linear-gradient(90deg, #0f3460, #0891b2);
    color: white;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 24px;
    position: sticky;
    top: 0;
    z-index: 1000;
  }
  header .logo {
    font-weight: 700;
    font-size: 1.5rem;
    letter-spacing: 1px;
    user-select: none;
  }
  header .header-left,
  header .header-right {
    display: flex;
    align-items: center;
  }
  header .header-left input[type="search"] {
    border-radius: 24px;
    border: none;
    padding: 8px 16px;
    font-size: 14px;
    outline: none;
    width: 240px;
    transition: width 0.3s ease;
  }
  header .header-left input[type="search"]:focus {
    width: 320px;
  }
  header .icon-button {
    background: none;
    border: none;
    color: white;
    cursor: pointer;
    position: relative;
    margin-left: 20px;
    font-size: 24px;
    user-select: none;
    display: flex;
    align-items: center;
  }
  header .icon-button .badge {
    position: absolute;
    top: 2px;
    right: 2px;
    background: #ef4444;
    color: white;
    font-size: 10px;
    font-weight: 700;
    border-radius: 9999px;
    padding: 2px 6px;
  }
  header .progress-overview {
    font-weight: 600;
    font-size: 14px;
    margin-left: 20px;
    user-select: none;
  }
  header .profile {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background: linear-gradient(135deg, #0891b2 0%, #0f3460 100%);
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 700;
    font-size: 18px;
    cursor: pointer;
    user-select: none;
  }

  /* Sidebar Left */
  #sidebar {
    grid-area: sidebar;
    border-right: 1px solid #e5e7eb;
    padding: 20px 16px;
    overflow-y: auto;
    background: #f9fafb;
  }
  #sidebar h2 {
    font-size: 1.2rem;
    font-weight: 700;
    margin-bottom: 16px;
    user-select: none;
  }
  #sidebar input[type="text"] {
    width: 100%;
    padding: 8px 12px;
    border-radius: 8px;
    border: 1px solid #d1d5db;
    margin-bottom: 20px;
    font-size: 14px;
  }
  #sidebar .course-list {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  #sidebar .course-list li {
    padding: 10px 12px;
    border-radius: 12px;
    margin-bottom: 8px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: space-between;
    transition: background-color 0.3s ease;
  }
  #sidebar .course-list li:hover,
  #sidebar .course-list li.active {
    background: #dbeafe;
  }
  #sidebar .course-list li .title {
    font-weight: 600;
    font-size: 14px;
    flex: 1;
  }
  #sidebar .course-list li .progress-ring {
    position: relative;
    width: 36px;
    height: 36px;
  }
  /* Progress ring SVG */
  .progress-ring circle {
    transition: stroke-dashoffset 0.35s;
    transform: rotate(-90deg);
    transform-origin: 50% 50%;
  }

  /* Middle Content */
  #main-content {
    grid-area: main;
    background: white;
    padding: 20px 32px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
  }
  #main-content h1 {
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: 12px;
    user-select: none;
  }
  #main-content .lesson-content {
    margin-bottom: 24px;
    flex: 1;
  }

  /* Video player container */
  .video-player-container {
    position: relative;
    max-width: 100%;
    border-radius: 12px;
    overflow: hidden;
    background: black;
    box-shadow: 0 4px 12px rgb(0 0 0 / 0.15);
    margin-bottom: 20px;
  }
  video {
    width: 100%;
    display: block;
  }
  /* Custom controls */
  .video-controls {
    background: rgba(255 255 255 / 0.85);
    display: flex;
    align-items: center;
    padding: 8px 16px;
    gap: 12px;
    user-select: none;
  }
  .video-controls button {
    background: none;
    border: none;
    cursor: pointer;
    color: #0891b2;
    font-size: 24px;
    padding: 4px;
  }
  .video-progress-container {
    flex: 1;
    position: relative;
    height: 6px;
    background: #e5e7eb;
    border-radius: 3px;
    cursor: pointer;
  }
  .video-progress-filled {
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    background: #0f3460;
    border-radius: 3px;
    width: 0%;
  }

  /* Transcript area */
  .transcript {
    margin-top: 12px;
    font-size: 14px;
    background: #f9fafb;
    border-radius: 8px;
    padding: 12px 16px;
    max-height: 160px;
    overflow-y: auto;
    color: #4b5563;
  }

  /* Quiz container */
  .quiz-container {
    margin-top: 12px;
    border-radius: 12px;
    padding: 24px;
    border: 1px solid #d1d5db;
    background: #f3f4f6;
  }
  .quiz-question {
    margin-bottom: 24px;
  }
  .quiz-question h3 {
    font-weight: 700;
    font-size: 16px;
    margin-bottom: 8px;
  }
  .quiz-options {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  .quiz-options li {
    margin-bottom: 8px;
  }
  .quiz-options label {
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 12px;
    font-size: 15px;
    user-select: none;
  }
  input[type="radio"],
  input[type="checkbox"] {
    cursor: pointer;
    accent-color: #0f3460;
  }
  /* Short answer */
  .quiz-short-answer input[type="text"] {
    width: 100%;
    border-radius: 8px;
    border: 1px solid #9ca3af;
    padding: 10px 12px;
    font-size: 14px;
  }
  .quiz-feedback {
    margin-top: 6px;
    font-weight: 600;
  }
  .quiz-feedback.correct {
    color: #22c55e;
  }
  .quiz-feedback.incorrect {
    color: #ef4444;
  }
  button.quiz-submit {
    background: #0f3460;
    border: none;
    color: white;
    padding: 12px 24px;
    border-radius: 16px;
    font-weight: 700;
    font-size: 16px;
    cursor: pointer;
    user-select: none;
    transition: background-color 0.3s ease;
  }
  button.quiz-submit:hover {
    background: #0891b2;
  }
  button.quiz-submit:disabled {
    background: #94a3b8;
    cursor: not-allowed;
  }
  /* Quiz score summary */
  .quiz-score {
    font-weight: 700;
    font-size: 16px;
    margin-top: 20px;
    user-select: none;
  }

  /* Right Sidebar */
  #right-sidebar {
    grid-area: right;
    background: #f9fafb;
    padding: 20px 16px;
    border-left: 1px solid #e5e7eb;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 24px;
  }
  #right-sidebar h2 {
    font-size: 1.2rem;
    font-weight: 700;
    user-select: none;
    margin-bottom: 12px;
  }
  /* Progress sidebar */
  .progress-sidebar {
    user-select: none;
  }
  .progress-bar {
    position: relative;
    height: 20px;
    background: #e5e7eb;
    border-radius: 12px;
    overflow: hidden;
  }
  .progress-bar-fill {
    height: 100%;
    background: #0891b2;
    border-radius: 12px 0 0 12px;
    width: 0%;
    transition: width 1s cubic-bezier(0.4, 0, 0.2, 1);
  }
  .progress-percent {
    margin-top: 4px;
    font-size: 14px;
    font-weight: 600;
    color: #374151;
  }
  /* Notes area */
  #notes-area {
    flex: 1;
    display: flex;
    flex-direction: column;
  }
  #notes-area textarea {
    resize: vertical;
    border-radius: 10px;
    border: 1px solid #d1d5db;
    padding: 12px;
    font-size: 14px;
    font-family: 'Inter', sans-serif;
    min-height: 80px;
    flex: 1;
  }
  #notes-area .btn-save {
    margin-top: 8px;
    background: #0f3460;
    border: none;
    color: white;
    padding: 10px;
    border-radius: 14px;
    font-weight: 700;
    cursor: pointer;
    user-select: none;
    transition: background-color 0.3s ease;
  }
  #notes-area .btn-save:disabled {
    background: #94a3b8;
    cursor: not-allowed;
  }
  #notes-area .btn-save:hover:not(:disabled) {
    background: #0891b2;
  }

  /* Discussion */
  #discussion-area {
    max-height: 220px;
    overflow-y: auto;
    background: white;
    border-radius: 12px;
    border: 1px solid #d1d5db;
    padding: 12px;
  }
  #discussion-area ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  #discussion-area li {
    border-bottom: 1px solid #e5e7eb;
    padding: 8px 0;
  }
  #discussion-area li:last-child {
    border-bottom: none;
  }
  .discussion-comment {
    font-size: 14px;
    color: #374151;
    user-select: text;
  }
  .discussion-header {
    font-weight: 600;
    font-size: 13px;
    color: #6b7280;
    margin-bottom: 6px;
  }
  #discussion-input {
    margin-top: 8px;
    display: flex;
    gap: 8px;
  }
  #discussion-input input[type="text"] {
    flex: 1;
    border: 1px solid #d1d5db;
    border-radius: 12px;
    padding: 8px 12px;
    font-size: 14px;
  }
  #discussion-input button {
    background: #0f3460;
    border: none;
    border-radius: 12px;
    padding: 8px 16px;
    color: white;
    font-weight: 700;
    cursor: pointer;
  }
  #discussion-input button:disabled {
    background: #94a3b8;
    cursor: not-allowed;
  }
  #discussion-input button:hover:not(:disabled) {
    background: #0891b2;
  }

  /* Resources links */
  #resources-area ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
  #resources-area li {
    margin-bottom: 8px;
  }
  #resources-area li a {
    font-weight: 600;
    font-size: 14px;
    color: #0891b2;
  }

  /* Assignment submission */
  #assignment-submission {
    margin-top: 16px;
    border-radius: 12px;
    padding: 16px;
    border: 1px solid #d1d5db;
    background: #f3f4f6;
  }
  #assignment-submission label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
  }
  #assignment-submission input[type="file"] {
    width: 100%;
  }
  #assignment-submission button.submit-btn {
    margin-top: 10px;
    background: #0f3460;
    border: none;
    border-radius: 14px;
    padding: 10px 20px;
    color: white;
    font-weight: 700;
    cursor: pointer;
    user-select: none;
    transition: background-color 0.3s ease;
  }
  #assignment-submission button.submit-btn:disabled {
    background: #94a3b8;
    cursor: not-allowed;
  }
  #assignment-submission button.submit-btn:hover:not(:disabled) {
    background: #0891b2;
  }

  /* Gradebook */
  #gradebook {
    margin-top: 24px;
  }
  #gradebook table {
    width: 100%;
    border-collapse: collapse;
    font-size: 14px;
  }
  #gradebook th,
  #gradebook td {
    border: 1px solid #d1d5db;
    padding: 8px 12px;
    text-align: left;
  }
  #gradebook th {
    background: #e5e7eb;
    font-weight: 700;
  }

  /* Study Scheduler */
  #study-scheduler {
    margin-top: 24px;
  }
  #study-scheduler h3 {
    margin-bottom: 12px;
  }
  #study-calendar {
    font-family: 'Inter', sans-serif;
    background: white;
    border-radius: 12px;
    padding: 16px;
    box-shadow: 0 4px 8px rgb(0 0 0 / 0.05);
    max-height: 300px;
    overflow-y: auto;
  }
  #study-calendar table {
    width: 100%;
    border-collapse: collapse;
    font-size: 14px;
  }
  #study-calendar th,
  #study-calendar td {
    border: 1px solid #d1d5db;
    padding: 8px 6px;
    text-align: center;
    user-select: none;
  }
  #study-calendar th {
    background: #e5e7eb;
    font-weight: 700;
  }
  #study-calendar td.deadline {
    background: #fde68a;
    cursor: pointer;
    font-weight: 700;
  }
  #study-calendar td.today {
    background: #dbeafe;
    font-weight: 700;
  }

  /* Flashcards */
  #flashcards {
    margin-top: 24px;
    user-select: none;
  }
  #flashcard {
    background: #f9fafb;
    border-radius: 16px;
    padding: 24px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    text-align: center;
    font-size: 18px;
    min-height: 120px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    cursor: pointer;
    user-select: none;
  }
  #flashcard .front, #flashcard .back {
    user-select: text;
  }
  #flashcard-buttons {
    margin-top: 16px;
    display: flex;
    gap: 16px;
    justify-content: center;
  }
  #flashcard-buttons button {
    padding: 12px 20px;
    border: none;
    border-radius: 14px;
    cursor: pointer;
    font-weight: 700;
    font-size: 14px;
    background: #0f3460;
    color: white;
    user-select: none;
    transition: background-color 0.3s ease;
  }
  #flashcard-buttons button:hover {
    background: #0891b2;
  }
  #flashcard-buttons button:disabled {
    background: #94a3b8;
    cursor: not-allowed;
  }

  /* Group Study Rooms */
  #group-study-rooms {
    margin-top: 24px;
  }
  #group-study-rooms ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  #group-study-rooms li {
    background: white;
    border-radius: 12px;
    padding: 12px 16px;
    margin-bottom: 12px;
    box-shadow: 0 2px 8px rgb(0 0 0 / 0.05);
    cursor: pointer;
    user-select: none;
  }

  #group-study-chat {
    background: white;
    border-radius: 12px;
    margin-top: 12px;
    padding: 12px;
    height: 150px;
    overflow-y: auto;
    font-size: 14px;
  }
  #group-study-message-input {
    margin-top: 8px;
    display: flex;
    gap: 8px;
  }
  #group-study-message-input input[type="text"] {
    flex: 1;
    padding: 8px 12px;
    border-radius: 12px;
    border: 1px solid #d1d5db;
    font-size: 14px;
  }
  #group-study-message-input button {
    background: #0f3460;
    border: none;
    border-radius: 12px;
    padding: 8px 16px;
    color: white;
    font-weight: 700;
    cursor: pointer;
  }
  #group-study-message-input button:disabled {
    background: #94a3b8;
    cursor: not-allowed;
  }
  #group-study-message-input button:hover:not(:disabled) {
    background: #0891b2;
  }

  /* Achievement badges & notifications */
  #achievements {
    margin-top: 24px;
  }
  .badge-list {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
  }
  .badge {
    border-radius: 16px;
    padding: 8px 12px;
    background: #0891b2;
    color: white;
    font-weight: 700;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    user-select: none;
    box-shadow: 0 4px 15px rgba(8 145 178 / 0.5);
    cursor: default;
  }
  .badge-icon {
    font-size: 18px;
  }
  /* Badge notification popup */
  #achievement-notification {
    position: fixed;
    top: 16px;
    right: 16px;
    background: #0891b2;
    color: white;
    padding: 16px 24px;
    border-radius: 16px;
    box-shadow: 0 4px 16px rgba(8 145 178 / 0.7);
    display: none;
    align-items: center;
    gap: 12px;
    font-weight: 700;
    user-select: none;
    z-index: 1100;
  }
  #achievement-notification .material-icons {
    font-size: 28px;
    animation: popAnimation 0.6s ease forwards;
  }
  @keyframes popAnimation {
    0% { transform: scale(0.5); opacity: 0; }
    50% { transform: scale(1.3); opacity: 1; }
    100% { transform: scale(1); opacity: 1; }
  }

  /* Scrollbar styling for webkit */
  ::-webkit-scrollbar {
    width: 10px;
    height: 10px;
  }
  ::-webkit-scrollbar-track {
    background: #f9fafb;
  }
  ::-webkit-scrollbar-thumb {
    background-color: #0891b2;
    border-radius: 10px;
  }
  
</style>
</head>
<body>
<div id="app">
  <header>
    <div class="header-left">
      <div class="logo" title="Koffan Maths Education Platform">Koffan Maths</div>
      <input type="search" placeholder="Search courses..." id="search-courses" aria-label="Search courses"/>
    </div>
    <div class="header-right" aria-label="Header actions">
      <button class="icon-button" title="Notifications" id="notifications-btn" aria-haspopup="true" aria-expanded="false" aria-label="View notifications">
        <span class="material-icons">notifications</span>
        <span class="badge" id="notifications-count" aria-live="polite">3</span>
      </button>
      <div class="progress-overview" aria-label="Progress overview" id="progress-overview">
        Progress: 0%
      </div>
      <div class="profile" tabindex="0" aria-label="User profile" id="user-profile" title="Logged in user: K. O"><span>K</span></div>
    </div>
  </header>

  <nav id="sidebar" aria-label="Course navigation">
    <h2>Courses</h2>
    <input type="text" id="filter-courses" placeholder="Filter by category or difficulty" aria-label="Filter courses"/>
    <ul class="course-list" id="course-list" role="listbox" aria-live="polite" aria-relevant="additions"></ul>

    <h2>My Study Plan</h2>
    <ul id="study-plan" aria-live="polite" aria-relevant="additions"></ul>
  </nav>

  <main id="main-content" tabindex="0" aria-live="polite">
    <h1 id="lesson-title" aria-label="Lesson title">Welcome to Koffan Maths</h1>
    <section class="lesson-content" id="lesson-content">
      <p>Select a course and lesson to start learning.</p>
    </section>
    <section id="video-section" hidden>
      <div class="video-player-container" aria-label="Video lesson player">
        <video id="video-player" preload="metadata" controls crossorigin="anonymous" playsinline>
          <source src="" type="video/mp4" />
          Sorry, your browser does not support embedded videos.
        </video>
      </div>
      <div class="transcript" id="video-transcript" aria-label="Video transcript" tabindex="0"></div>
    </section>
    <section id="quiz-section" hidden aria-live="polite" aria-atomic="true"></section>
  </main>

  <aside id="right-sidebar" aria-label="Lesson sidebar">
    <section class="progress-sidebar" aria-live="polite" aria-atomic="true">
      <h2>Course Progress</h2>
      <div class="progress-bar" aria-label="Course progress bar">
        <div class="progress-bar-fill" id="course-progress-bar"></div>
      </div>
      <div class="progress-percent" id="course-progress-percent">0%</div>
    </section>

    <section id="notes-area" aria-label="Note taking area">
      <h2>Notes</h2>
      <textarea id="notes-textarea" placeholder="Write your notes here..." aria-multiline="true" rows="6"></textarea>
      <button class="btn-save" id="notes-save-btn" disabled>Save Note</button>
    </section>

    <section id="discussion-area" aria-label="Discussion forum">
      <h2>Discussion</h2>
      <ul id="discussion-list"></ul>
      <div id="discussion-input">
        <input type="text" id="discussion-text" placeholder="Add a comment..." aria-label="Add a comment"/>
        <button id="discussion-submit" disabled>Post</button>
      </div>
    </section>

    <section id="resources-area" aria-label="Lesson resources">
      <h2>Resources</h2>
      <ul id="resources-list"></ul>
    </section>

    <section id="assignment-submission" aria-label="Assignment submission">
      <h2>Submit Assignment</h2>
      <label for="assignment-file">Upload File</label>
      <input type="file" id="assignment-file" aria-describedby="assignment-desc" />
      <button class="submit-btn" id="assignment-submit-btn" disabled>Submit</button>
      <p id="assignment-desc" style=