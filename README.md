<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Attendance Tracker</title>

    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
        }

        body {
            min-height: 100vh;
            background: #f2f4f7;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 900px;
            min-height: 550px;
            background: white;
            border-radius: 15px;
            overflow: hidden;
            display: flex;
            box-shadow: 0 5px 20px rgba(0, 0, 0, 0.15);
        }

        /* LEFT SIDE */
        .input-section {
            width: 50%;
            padding: 50px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .input-section h1 {
            font-size: 32px;
            margin-bottom: 10px;
        }

        .input-section p {
            color: #666;
            margin-bottom: 25px;
        }

        input {
            width: 100%;
            padding: 16px;
            border: 1px solid #ccc;
            border-radius: 8px;
            font-size: 16px;
            margin-bottom: 10px;
            outline: none;
        }

        input:focus {
            border-color: #222;
        }

        button {
            width: 100%;
            padding: 16px;
            border: none;
            border-radius: 8px;
            background: #222;
            color: white;
            font-size: 16px;
            cursor: pointer;
        }

        button:active {
            transform: scale(0.98);
        }

        /* RIGHT SIDE */
        .attendance-section {
            width: 50%;
            background: #f8f9fa;
            padding: 40px;
            border-left: 1px solid #ddd;
        }

        .attendance-section h2 {
            margin-bottom: 20px;
        }

        #attendanceList {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .person {
            background: white;
            padding: 15px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.08);
            font-size: 17px;
        }

        .empty {
            color: #888;
            font-style: italic;
        }


        /* 📱 PHONE SCREEN */
        @media (max-width: 600px) {

            body {
                padding: 10px;
                align-items: flex-start;
            }

            .container {
                flex-direction: column;
                min-height: auto;
                margin-top: 10px;
            }

            .input-section {
                width: 100%;
                padding: 30px 20px;
            }

            .input-section h1 {
                font-size: 26px;
            }

            .attendance-section {
                width: 100%;
                padding: 25px 20px;
                border-left: none;
                border-top: 1px solid #ddd;
                min-height: 300px;
            }

            input {
                font-size: 16px;
                padding: 15px;
            }

            button {
                font-size: 16px;
                padding: 15px;
            }
        }
    </style>
</head>

<body>

    <div class="container">

        <!-- INPUT -->
        <div class="input-section">

            <h1>Attendance Tracker</h1>

            <p>
                Enter your name to mark your attendance.
            </p>

            <input
                type="text"
                id="nameInput"
                placeholder="Enter your name"
                autocomplete="off"
            >

            <button onclick="toggleAttendance()">
                Mark Attendance
            </button>

        </div>


        <!-- ATTENDANCE BOARD -->
        <div class="attendance-section">

            <h2>Present Today</h2>

            <div id="attendanceList">

                <div class="empty">
                    No one is present yet.
                </div>

            </div>

        </div>

    </div>


    <script>

        let attendance = [];


        function toggleAttendance() {

            const input = document.getElementById("nameInput");

            const name = input.value.trim();


            // Don't allow empty names
            if (name === "") {
                alert("Please enter your name.");
                return;
            }


            // Check if the name already exists
            const existingIndex = attendance.findIndex(
                person =>
                person.toLowerCase() === name.toLowerCase()
            );


            if (existingIndex !== -1) {

                // Already present → remove name
                attendance.splice(existingIndex, 1);

            } else {

                // Not present → add name
                attendance.push(name);

            }


            // Clear input
            input.value = "";


            // Update attendance board
            updateBoard();
        }


        function updateBoard() {

            const list =
                document.getElementById("attendanceList");


            list.innerHTML = "";


            // Nobody present
            if (attendance.length === 0) {

                list.innerHTML =
                    '<div class="empty">' +
                    'No one is present yet.' +
                    '</div>';

                return;
            }


            // Display names
            attendance.forEach(function(name) {

                const person =
                    document.createElement("div");

                person.className = "person";

                person.textContent = name;

                list.appendChild(person);

            });
        }


        // Allow pressing ENTER
        document
            .getElementById("nameInput")
            .addEventListener("keypress", function(event) {

                if (event.key === "Enter") {
                    toggleAttendance();
                }

            });

    </script>

</body>
</html>
