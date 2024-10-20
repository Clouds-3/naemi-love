<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Love You</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding-top: 50px;
        }
        .strikethrough {
            text-decoration: line-through;
        }
        .names {
            font-size: 20px;
            margin-bottom: 20px;
        }
        .result {
            font-size: 24px;
            font-weight: bold;
            margin-top: 20px;
        }
        .animation-container {
            margin-top: 20px;
            font-size: 18px;
        }
        .flames-letters {
            font-size: 30px;
            margin-top: 10px;
        }
        .highlight {
            transition: color 1s ease, opacity 1s ease;
            color: red;
        }
        .fade-out {
            opacity: 0;
        }
    </style>
</head>
<body>
    <h1>FLAMES</h1>
    
    <div class="names">
        <table align="center">
            <tr>
                <td><p>👨 :</p></td>
                <td><span id="name1" >Naemi Raja</span></td>
            </tr>
            <tr>
                <td><p>👩 :</p></td>
                <td><span id="name2">Deva Benadict Wilzcy</span></td>
            </tr>
        </table>
    </div>

    <h2>Striked:</h2>
    <p id="commonLetters"></p>

    <div class="animation-container">
        <h2>Elimination Process:</h2>
        <div class="flames-letters" id="flamesLetters">F L A M E S</div>
        <div id="flamesResult" class="result"></div>
    </div>
    <h2>Just Understand Thizz❤️</h2>

    <script>
        // Static names
        let name1 = "naemiraja".toLowerCase();
        let name2 = "devabenadictwilzcy".toLowerCase();

        // Function to calculate common letters and FLAMES result
        function calculateFlames() {
            // Convert names to arrays
            let name1Arr = name1.split('');
            let name2Arr = name2.split('');

            // Find and strike common letters
            let commonLettersHTML = '';
            let balanceLettersCount = 0;

            for (let i = 0; i < name1Arr.length; i++) {
                if (name2Arr.includes(name1Arr[i])) {
                    commonLettersHTML += '<span class="strikethrough">' + name1Arr[i] + '</span>';
                    name2Arr.splice(name2Arr.indexOf(name1Arr[i]), 1);  // Remove common letter from name2Arr
                } else {
                    commonLettersHTML += name1Arr[i];
                    balanceLettersCount++;
                }
            }

            // Add remaining letters from name2Arr
            for (let j = 0; j < name2Arr.length; j++) {
                commonLettersHTML += name2Arr[j];
                balanceLettersCount++;
            }

            // Display the common letters (with strike-through)
            document.getElementById('commonLetters').innerHTML = commonLettersHTML;

            // Start the FLAMES elimination animation
            animateFlames(balanceLettersCount);
        }

        function animateFlames(lettersCount) {
            let flames = ['F', 'L', 'A', 'M', 'E', 'S'];
            let index = 0;
            let flamesDiv = document.getElementById('flamesLetters');
            let resultDiv = document.getElementById('flamesResult');

            let flamesMeaning = {
                'F': 'Friends',
                'L': 'Love',
                'A': 'Affection',
                'M': 'Marriage',
                'E': 'Enemy',
                'S': 'Siblings'
            };

            function eliminate() {
                if (flames.length > 1) {
                    index = (index + lettersCount - 1) % flames.length;
                    let eliminatedLetter = flames.splice(index, 1);  // Remove one option

                    // Highlight the letter before removing it
                    let highlightedHTML = flames.join(' ') + ' <span class="highlight">' + eliminatedLetter + '</span>';
                    flamesDiv.innerHTML = highlightedHTML;  // Update display with highlight
                    setTimeout(() => {
                        flamesDiv.classList.add('fade-out');  // Add fade animation
                        setTimeout(() => {
                            flamesDiv.classList.remove('fade-out');  // Reset fade-out
                            flamesDiv.innerHTML = flames.join(' ');  // Remove the eliminated letter from display

                            // Continue elimination if more letters are left
                            if (flames.length > 1) {
                                eliminate();
                            } else {
                                resultDiv.innerText = 'Result: ' + flamesMeaning[flames[0]];  // Display final result
                            }
                        }, 1000);  // Wait for fade-out to complete
                    }, 1000);  // Wait for highlight to complete
                }
            }

            eliminate();  // Start elimination process
        }

        // Call the function to start the FLAMES calculation
        calculateFlames();
    </script>
</body>
</html>
