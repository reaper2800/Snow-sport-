# Fully delete all old Clue 3 logic and implement the correct target shooting version

# Manually reconstruct the correct Clue 3 section and ensure JS is fully updated
rebuilt_clue3_target_game_html = rebuilt_unscramble_html.replace(
    # Remove old clue 3 unscramble HTML block
    """
    <div class="clue-box hidden" id="game3">
      <h3>Clue 3 Puzzle: Unscramble the Word</h3>
      <p>Unscramble this word: <strong>istnfracture</strong></p>
      <button onclick="showHint(3)">Hint</button>
      <p id="hint3" class="hidden"><em>It supports buildings, roads, and services.</em></p>
      <input type="text" id="scrambleInput" placeholder="Type your answer here">
      <button onclick="checkScramble()">Submit</button>
    </div>
    """,
    # Replace with new Clue 3 shooting game
    """
    <div class="clue-box hidden" id="game3">
      <h3>Clue 3 Mini-Game: Shoot the Correct Target</h3>
      <p>Click the correct target labeled "Infrastructure" to move on.</p>
      <button onclick="showHint(3)">Hint</button>
      <p id="hint3" class="hidden"><em>It supports roads, buildings, and services.</em></p>
      <div style="margin-top: 10px;">
        <button class="target" onclick="checkTarget3(this)">Recreation</button>
        <button class="target" onclick="checkTarget3(this)">Infrastructure</button>
        <button class="target" onclick="checkTarget3(this)">Tourism</button>
        <button class="target" onclick="checkTarget3(this)">Snowfall</button>
      </div>
    </div>
    """
).replace(
    # Remove the checkScramble function entirely and insert the new one
    """
    function checkScramble() {
      const input = document.getElementById('scrambleInput').value.trim().toLowerCase();
      if (input === 'infrastructure') {
        clues.c3 = true;
        document.getElementById('game3').classList.add('hidden');
        document.getElementById('clue4').classList.remove('hidden');
      } else {
        alert('Nope! Try again.');
      }
    }
    """,
    """
    function checkTarget3(button) {
      if (button.textContent.trim().toLowerCase() === 'infrastructure') {
        clues.c3 = true;
        document.getElementById('game3').classList.add('hidden');
        document.getElementById('clue4').classList.remove('hidden');
      } else {
        alert('Try again! That’s not the right one.');
      }
    }
    """
)

# Save and zip the clean final version
final_clean_target_file = "/mnt/data/index.html"
final_clean_target_zip = "/mnt/data/utah_snow_sports_final_clue3_target.zip"

with open(final_clean_target_file, "w") as f:
    f.write(rebuilt_clue3_target_game_html)

with zipfile.ZipFile(final_clean_target_zip, "w") as zipf:
    zipf.write(final_clean_target_file, arcname="index.html")

final_clean_target_zip
