<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Love Letter</title>
  <style>
    :root {
      --accent: #c97c5d;
      --background: #f6efe9;
      --text-color: #4b3f36;
      --button-color: #c97c5d;
    }
    body { margin: 0; font-family: 'Georgia', serif; background-color: var(--background); color: var(--text-color); overflow-x: hidden; }
    h1, p { line-height: 1.5; }
    .greeting { position: fixed; inset: 0; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; padding: 24px; background: linear-gradient(180deg, #f6efe9, #f1e3d8); z-index: 10; animation: fadeIn 1s ease; }
    .greeting h1 { font-size: 2.5rem; margin-bottom: 10px; }
    .greeting p { max-width: 420px; opacity: 0.9; margin-bottom: 20px; font-size: 1.1rem; }
    .greeting button { padding: 12px 24px; border: none; border-radius: 10px; background-color: var(--button-color); color: #fff; font-size: 1rem; cursor: pointer; transition: transform 0.3s; }
    .greeting button:hover { transform: scale(1.05); }

    .container { display: none; padding: 24px; text-align: center; }

    .envelope { width: 150px; height: 100px; background: var(--accent); margin: 50px auto; border-radius: 12px; cursor: pointer; display: flex; align-items: center; justify-content: center; color: #fff; font-weight: bold; box-shadow: 0 6px 12px rgba(0,0,0,0.1); transition: transform 0.3s; }
    .envelope:hover { transform: translateY(-5px); }

    .letter { display: none; max-width: 600px; margin: 20px auto; padding: 30px; background: #fff3e6; border-radius: 16px; text-align: left; animation: fadeIn 1s ease; box-shadow: 0 8px 16px rgba(0,0,0,0.1); font-size: 1.1rem; }
    .letter p { margin-bottom: 15px; }
    .letter button { margin-top: 20px; padding: 10px 20px; border-radius: 8px; border: none; background-color: var(--button-color); color: #fff; cursor: pointer; font-size: 1rem; }

    .questions { display: none; margin: 20px auto; max-width: 500px; text-align: center; font-size: 1.1rem; }
    .questions button { margin: 8px; padding: 10px 22px; border-radius: 12px; border: none; cursor: pointer; background-color: var(--button-color); color: #fff; font-size: 1rem; transition: transform 0.2s; }
    .questions button:hover { transform: scale(1.05); }
    .response { margin-top: 16px; min-height: 24px; font-style: italic; color: #6b4f3a; }

    .gallery { display: none; max-width: 800px; margin: 40px auto; text-align: center; }
    .gallery img { width: 90%; max-width: 400px; margin: 20px auto; border-radius: 16px; box-shadow: 0 6px 12px rgba(0,0,0,0.1); }

    @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
  </style>
</head>
<body>

<div class="greeting" id="greeting">
  <h1>Happy New Year</h1>
  <p>This isn’t an ending<br>it’s the end of the beginning.</p>
  <button onclick="startExperience()">Continue the story</button>
</div>

<div class="container">
  <div class="envelope" onclick="openEnvelope()">Open Envelope</div>

  <div class="letter" id="letter">
    <p>Hey dumbo,</p>
    <p>I know we didn't start the year together, but I want to end it with you and all the years awaiting.</p>
    <p>I want to be with you, learn and experience many more things together:<br>
    - Re-watch Stranger Things and Harry Potter marathons<br>
    - Tease each other<br>
    - See each other’s flaws<br>
    - Watch and support you through every cricket match<br>
    - Brag about you to my friends<br>
    - Or maybe marry each other, ahemm…</p>
    <p>Well, I don’t know how stories usually begin, but this is ours. Even though it’s only been a few weeks, every moment with you feels like something I’ve been waiting for.</p>
    <p>I don’t know what the next chapter will bring, but I hope I get to be in every one of them with you.</p>
    <p>Here’s to the end of the beginning and all that comes next.</p>
    <p>Love,<br>Your Amine</p>
    <button onclick="showQuestions()">Next</button>
  </div>

  <div class="questions" id="questions">
    <p id="questionText">Up for Harry Potter and Stranger Things trivia someday?</p>
    <button onclick="answerYes()">Yes</button>
    <button onclick="answerNo()">No</button>
    <div class="response" id="responseText"></div>
  </div>

  <div class="gallery" id="gallery">
    <img src="photos/photo1.jpg" alt="Jersey Memory">
    <img src="photos/photo2.jpg" alt="First Photo of You">
    <img src="photos/photo3.jpg" alt="Farewell Photo">
    <img src="photos/photo4.jpg" alt="Memory 4">
    <img src="photos/photo5.jpg" alt="Memory 5">
  </div>
</div>

<script>
  function startExperience() {
    document.getElementById('greeting').style.display = 'none';
    document.querySelector('.container').style.display = 'block';
  }

  function openEnvelope() {
    document.querySelector('.envelope').style.display = 'none';
    document.getElementById('letter').style.display = 'block';
  }

  function showQuestions() {
    document.getElementById('letter').style.display = 'none';
    document.getElementById('questions').style.display = 'block';
    currentQuestion = 0;
    nextQuestion();
  }

  const questions = [
    { text: 'Up for Harry Potter and Stranger Things trivia someday?', yes: 'Hell yeah, I am ready with my wand and demogorgon knowledge to beat you up', no: 'Well… we’ll make time for it eventually' },
    { text: 'Ready to bear more of my mood swings?', yes: 'I guess I\'ll be more moody than', no: 'Even if you say no, I still love you' },
    { text: 'Can I be your grammar corrector forever?', yes: 'Of course you chose yes baby, what would you do without me~', no: 'Okay, but I’ll still try to impress you with my grammar' },
    { text: 'Can I be your partner in every season?', yes: 'Every season, every chapter — count me in', no: 'Even if you say no, I still want to share the seasons with you' },
    { text: 'And lastly, wanna be stuck together forever?', yes: 'I’m so glad we’re stuck together forever', no: 'I’m so glad we’re stuck together forever' }
  ];

  let currentQuestion = 0;

  function nextQuestion() {
    if(currentQuestion < questions.length) {
      document.getElementById('questionText').innerText = questions[currentQuestion].text;
      document.getElementById('responseText').innerText = '';
    } else {
      document.getElementById('questions').style.display = 'none';
      document.getElementById('gallery').style.display = 'block';
    }
  }

  function answerYes() {
    document.getElementById('responseText').innerText = questions[currentQuestion].yes;
    currentQuestion++;
    setTimeout(nextQuestion, 1500);
  }

  function answerNo() {
    document.getElementById('responseText').innerText = questions[currentQuestion].no;
    currentQuestion++;
    setTimeout(nextQuestion, 1500);
  }
</script>
</body>
</html>
