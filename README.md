# SapmiTTS
Speech native Sápmi in Text Audio




const textInput = document.getElementById('textInput');
const speakButton = document.getElementById('speakButton');
const recognizedText = document.getElementById('recognizedText');
const listenButton = document.getElementById('listenButton');

// TTS
const synth = window.speechSynthesis;

speakButton.addEventListener('click', () => {
    const text = textInput.value;
    const utterance = new SpeechSynthesisUtterance(text);

    // ***IMPORTANT: Set the correct language code for your Sami dialect here!***
    // Check browser compatibility and available voices for Sami.
    // Example (Northern Sami - you'll need to verify the correct code):
    utterance.lang = 'sme';  // Or the appropriate code.  Test thoroughly!

    synth.speak(utterance);
});


// STT (Speech Recognition)
const recognition = new webkitSpeechRecognition() || new SpeechRecognition(); // Browser prefixes

recognition.lang = 'sme'; //  ***CRITICAL: Sami language support is essential here!***

listenButton.addEventListener('click', () => {
    recognition.start();
});

recognition.onresult = (event) => {
    const transcript = event.results[0][0].transcript;
    recognizedText.value = transcript;
};

recognition.onerror = (event) => {
    console.error("Speech recognition error:", event.error);
    alert("Speech recognition error. Check console for details. Sami language support may be limited.");
};
