<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TRAP MASTER PRO | TRUNKBANG LLC</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Archivo+Black&display=swap');
        .metallic-text {
            background: linear-gradient(to bottom, #fff 20%, #888 50%, #444 80%, #222 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(2px 4px 6px rgba(0,0,0,0.8));
        }
    </style>
</head>
<body class="bg-black text-white font-['Archivo_Black']">

    <div class="min-h-screen flex flex-col items-center justify-center p-6 text-center">
        <h1 class="text-7xl md:text-9xl italic uppercase metallic-text tracking-tighter mb-2">TRAP MASTER</h1>
        <p class="text-red-600 tracking-[0.3em] font-bold mb-10 text-sm">INSTANT AI MIX & MASTER | POWERED BY TRUNKBANG</p>

        <div id="drop-zone" class="w-full max-w-2xl p-12 border-4 border-double border-zinc-700 bg-zinc-900 rounded-3xl shadow-[0_0_100px_rgba(255,255,255,0.05)] relative overflow-hidden">
            <div class="absolute inset-0 opacity-10 pointer-events-none" style="background-image: url('https://www.transparenttextures.com/patterns/carbon-fibre.png');"></div>
            
            <div class="relative z-10">
                <div class="mb-8 text-6xl">💎</div>
                <h2 class="text-2xl mb-6 text-zinc-300 uppercase">Upload your raw heat</h2>
                
                <input type="file" id="audio-input" class="hidden" accept="audio/*">
                <button onclick="document.getElementById('audio-input').click()" 
                        class="bg-gradient-to-r from-red-600 via-red-500 to-red-800 px-12 py-5 rounded-lg border-2 border-white text-2xl italic hover:scale-110 transition-transform shadow-[0_10px_20px_rgba(220,38,38,0.5)]">
                    SELECT AUDIO FILE
                </button>
            </div>
        </div>

        <div class="mt-16 flex flex-wrap justify-center gap-8 opacity-40 grayscale hover:grayscale-0 transition-all duration-700 text-[10px] tracking-widest uppercase">
            <div class="border border-white p-1 px-3">TRUNKBANG LLC</div>
            <div class="border border-white p-1 px-3">DISTROKID</div>
            <div class="border border-white p-1 px-3">HEADQUARTERS BARBER</div>
            <div class="border border-white p-1 px-3">E.N.S. PLUS</div>
        </div>
    </div>

    // 1. Initialize the Cloudinary Widget
const myWidget = cloudinary.createUploadWidget({
  cloudName: 'YOUR_CLOUD_NAME_HERE', 
  uploadPreset: 'YOUR_PRESET_NAME',
  folder: 'trap_master_uploads',
  // This is the "Secret Sauce" - The Transformation String
  // 'e_volume:10' cranks the gain, 'e_equalizer' boosts the low end (Bass)
  transformation: [
    {effect: "volume:10"},
    {effect: "equalizer:0:0:0:50:50:50:0:0:0:0"} 
  ]
}, (error, result) => { 
    if (!error && result && result.event === "success") { 
      console.log('Done! Here is the mastered track: ', result.info.secure_url);
      
      // Update the UI to show the "Download Mastered" button
      document.getElementById('drop-zone').innerHTML = `
        <h2 class="text-3xl text-yellow-400 mb-6 italic">TRACK MASTERED 💎</h2>
        <a href="${result.info.secure_url}" target="_blank" 
           class="bg-white text-black px-8 py-4 rounded-full font-black uppercase hover:bg-yellow-400 transition-all">
           Download the Heat
        </a>
        <p class="mt-4 text-xs text-zinc-500">TRUNKBANG LLC SECURED</p>
      `;
    }
});

// 2. Link it to your big red button
document.getElementById('audio-input-btn').addEventListener("click", function(){
    myWidget.open();
}, false);

