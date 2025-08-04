<script type="text/javascript">
        var gk_isXlsx = false;
        var gk_xlsxFileLookup = {};
        var gk_fileData = {};
        function filledCell(cell) {
          return cell !== '' && cell != null;
        }
        function loadFileData(filename) {
        if (gk_isXlsx && gk_xlsxFileLookup[filename]) {
            try {
                var workbook = XLSX.read(gk_fileData[filename], { type: 'base64' });
                var firstSheetName = workbook.SheetNames[0];
                var worksheet = workbook.Sheets[firstSheetName];

                // Convert sheet to JSON to filter blank rows
                var jsonData = XLSX.utils.sheet_to_json(worksheet, { header: 1, blankrows: false, defval: '' });
                // Filter out blank rows (rows where all cells are empty, null, or undefined)
                var filteredData = jsonData.filter(row => row.some(filledCell));

                // Heuristic to find the header row by ignoring rows with fewer filled cells than the next row
                var headerRowIndex = filteredData.findIndex((row, index) =>
                  row.filter(filledCell).length >= filteredData[index + 1]?.filter(filledCell).length
                );
                // Fallback
                if (headerRowIndex === -1 || headerRowIndex > 25) {
                  headerRowIndex = 0;
                }

                // Convert filtered JSON back to CSV
                var csv = XLSX.utils.aoa_to_sheet(filteredData.slice(headerRowIndex)); // Create a new sheet from filtered array of arrays
                csv = XLSX.utils.sheet_to_csv(csv, { header: 1 });
                return csv;
            } catch (e) {
                console.error(e);
                return "";
            }
        }
        return gk_fileData[filename] || "";
        }
        </script><!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Junior Developer Portfolio</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f9;
            color: #333;
        }
        header {
            background-color: #2c3e50;
            color: white;
            text-align: center;
            padding: 2rem;
        }
        header h1 {
            margin: 0;
            font-size: 2.5rem;
        }
        header p {
            margin: 0.5rem 0;
            font-size: 1.2rem;
        }
        nav {
            background-color: #34495e;
            padding: 1rem;
        }
        nav a {
            color: white;
            text-decoration: none;
            margin: 0 1rem;
            font-size: 1rem;
        }
        nav a:hover {
            text-decoration: underline;
        }
        section {
            padding: 2rem;
            max-width: 1000px;
            margin: 0 auto;
        }
        h2 {
            color: #2c3e50;
            border-bottom: 2px solid #3498db;
            padding-bottom: 0.5rem;
        }
        .skills ul {
            list-style: none;
            padding: 0;
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
        }
        .skills li {
            background-color: #3498db;
            color: white;
            padding: 0.5rem 1rem;
            border-radius: 5px;
        }
        .projects {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
        }
        .project-card {
            background-color: white;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            padding: 1rem;
        }
        .project-card h3 {
            margin: 0;
            color: #2c3e50;
        }
        .project-card p {
            margin: 0.5rem 0;
        }
        .project-card a {
            color: #3498db;
            text-decoration: none;
        }
        .project-card a:hover {
            text-decoration: underline;
        }
        .contact p {
            margin: 0.5rem 0;
        }
        .contact a {
            color: #3498db;
            text-decoration: none;
        }
        .contact a:hover {
            text-decoration: underline;
        }
        footer {
            background-color: #2c3e50;
            color: white;
            text-align: center;
            padding: 1rem;
            position: relative;
            bottom: 0;
            width: 100%;
        }
        @media (max-width: 600px) {
            header h1 {
                font-size: 1.8rem;
            }
            nav a {
                display: block;
                margin: 0.5rem 0;
            }
            .projects {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>Kennedy Muriithi</h1>
        <p>Junior Developer | Passionate about Building Web Applications</p>
    </header>
    <nav>
        <a href="#about">About</a>
        <a href="#skills">Skills</a>
        <a href="#projects">Projects</a>
        <a href="#contact">Contact</a>
    </nav>
    <section id="about">
        <h2>About Me</h2>
        <p>Hello! I'm Kennedy Muriithi, a junior developer with a passion for creating user-friendly web applications. I specialize in front-end development with a focus on HTML, CSS, and JavaScript. I enjoy learning new technologies and applying them to solve real-world problems. My goal is to contribute to innovative projects while continuously growing my skills.</p>
    </section>
    <section id="skills" class="skills">
        <h2>Skills</h2>
        <ul>
            <li>HTML5</li>
            <li>CSS3</li>
            <li>JavaScript</li>
            <li>React</li>
            <li>Git</li>
            <li>Responsive Design</li>
            <li>Python</li>
            <li>Node.js</li>
        </ul>
    </section>
    <section id="projects" class="projects">
        <h2>Projects</h2>
        <div class="project-card">
            <h3>Todo List App</h3>
            <p>A simple, responsive todo list application built with React and local storage to manage tasks efficiently.</p>
            <p><a href="https://github.com/KMbugu/todolist" target="_blank">View on GitHub</a></p>
        </div>
        <div class="project-card">
            <h3>Weather Dashboard</h3>
            <p>A web app that fetches real-time weather data using a public API, styled with CSS and built with JavaScript.</p>
            <p><a href="https://github.com/KMbugu/weather-dashboard" target="_blank">View on GitHub</a></p>
        </div>
        <div class="project-card">
            <h3>Personal Blog</h3>
            <p>A static blog site built with HTML, CSS, and JavaScript, featuring a clean design and markdown support.</p>
            <p><a href="https://github.com/KMbugu/personal-blog" target="_blank">View on GitHub</a></p>
        </div>
    </section>
    <section id="contact" class="contact">
        <h2>Contact</h2>
        <p>Email: <a href="mailto:kmmuriithi@gmail.com">kmmuriithi@gmail.com.com</a></p>
        <p>LinkedIn: <a href="https://linkedin.com/in/Kennedy Muriithi" target="_blank">linkedin.com/in/Kennedy Muriithi</a></p>
        <p>GitHub: <a href="https://github.com/KMbugu" target="_blank">github.com/KMbugu</a></p>
    </section>
    <footer>
        <p>&copy; 2025 Kennedy Muriithi. All rights reserved.</p>
    </footer>
</body>
</html>
