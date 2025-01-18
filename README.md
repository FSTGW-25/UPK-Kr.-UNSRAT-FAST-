
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menampilkan PDF Berdasarkan Dwibulan dan Bidang</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #E5CEE8, #D4B8D1); /* Gradasi warna E5CEE8 dan warna lebih gelap */
            padding: 20px;
            margin: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
        }

        .container {
            max-width: 800px;
            margin: auto;
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            flex-grow: 1; /* Agar container tetap memanjang */
        }

        h1 {
            text-align: center;
            margin-bottom: 20px;
        }

        #calendar {
            margin-top: 20px;
        }

        footer {
            display: flex;
            justify-content: center;
            align-items: center;
            margin-top: 40px;
            padding: 20px 0;
            border-top: 1px solid #ddd;
        }

        footer img {
            width: 100px; /* Menyesuaikan ukuran gambar agar tidak terlalu besar */
            height: auto;
        }

        .footer-box {
            text-align: center;
            margin-top: 40px;
        }

        .footer-box img {
            width: 100%;
            max-width: 800px;
            height: auto;
        }

        .calendar-header {
            text-align: center;
            font-size: 28px;
            font-weight: bold;
            margin-top: 20px;
            font-family: 'Arial', sans-serif;
        }

        .button-container {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }

        .button-container button {
            padding: 10px 15px;
            font-size: 16px;
            cursor: pointer;
            background-color: #E5CEE8; /* Warna lilac */
            color: black;
            border: none;
            border-radius: 5px;
        }

        .button-container button:hover {
            background-color: #D4B8D1;
            color: white;
        }

        /* Style untuk tombol bidang */
        .button-container-bidang {
            display: none;
            flex-direction: column;
            margin-top: 20px;
            padding: 15px;
            background-color: #f3e6f9; /* Latar belakang yang lebih lembut */
            border-radius: 10px; /* Membuat sudut kotak lebih melengkung */
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); /* Bayangan ringan di sekitar kontainer */
        }

        .site-header {
    display: none;
}

        .button-container-bidang button {
    margin-bottom: 12px;
    background: linear-gradient(135deg, #E5CEE8, #A1C9FF); /* Lilac ke Biru Laut Muda */
    color: #000000; /* Mengubah warna teks menjadi hitam */
    font-family: 'Arial', sans-serif; /* Font yang mudah dibaca */
    font-size: 18px; /* Ukuran font yang sedikit lebih besar */
    padding: 10px 20px; /* Memberikan ruang di dalam tombol */
    border: none; /* Menghilangkan border default tombol */
    border-radius: 5px; /* Membuat tombol memiliki sudut melengkung */
    cursor: pointer; /* Menunjukkan bahwa tombol bisa diklik */
    transition: background-color 0.3s ease, box-shadow 0.3s ease; /* Efek transisi saat hover dan saat tombol aktif */
}

/* Efek hover untuk tombol */
.button-container-bidang button:hover {
    background-color: #3a3ac0; /* Warna tombol sedikit lebih gelap saat hover */
    box-shadow: 0 0 10px 3px rgba(255, 255, 255, 0.6); /* Efek cahaya putih lembut saat hover */
}

/* Efek saat tombol diklik */
.button-container-bidang button:active {
    box-shadow: 0 0 20px 6px rgba(255, 255, 255, 0.9); /* Efek cahaya lebih kuat saat tombol ditekan */
}



        .notification-box {
    text-align: center;
    margin-top: 20px;
    padding: 20px;
    border-radius: 10px;
    background-color: #FFF6D5; /* Warna kuning lembut */
    border: 1px solid #FFB700; /* Garis kuning terang */
    color: #6B5200; /* Warna teks kuning gelap */
    font-size: 16px;
    font-family: 'Arial', sans-serif;
    font-weight: bold;
}

.notification-box span {
    font-style: italic;
}

        /* Style untuk tombol yang aktif */
        .button-container button.active {
            background-color: #D4B8D1;
            color: white;
        }

       
    #pdfViewer embed {
        margin-top: 20px;
    }

    /* Music Box */
    .music-box {
      background-color: #333;
      color: white;
      width: 300px;
      margin: 20px auto;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(255, 255, 255, 0.3);
      text-align: center;
    }

    .music-box h2 {
      font-size: 1.5em;
      margin: 0;
    }

    .cover-circle {
      width: 150px;
      height: 150px;
      margin: 20px auto;
      border-radius: 50%;
      background: url('pengurus.jpeg') no-repeat center center;
      background-size: cover;
      animation: rotateCover 8s linear infinite;
      box-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
    }

    @keyframes rotateCover {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    .progress-container {
      width: 100%;
      background-color: #444;
      height: 5px;
      border-radius: 5px;
      position: relative;
      margin-top: 20px;
    }

    .progress-bar {
      height: 100%;
      background-color: #4CAF50;
      width: 0;
      border-radius: 5px;
      transition: width 0.2s ease;
    }

    .time-container {
      display: flex;
      justify-content: space-between;
      font-size: 0.8em;
      color: #bbb;
      margin-top: 5px;
    }

    .controls {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
    }

    .control-btn {
      width: 50px;
      height: 50px;
      border: none;
      background-color: transparent;
      border-radius: 50%;
      color: white;
      font-size: 1.5em;
      cursor: pointer;
      box-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
    }

    .control-btn:hover {
      background-color: #555;
    }



    </style>
</head>
<body>
   

    <div class="container">
        <div id="calendar"></div>

        <!-- Box footer dengan gambar -->
        <div class="footer-box">
            <img src="web 2.jpeg" alt="Footer Image">
        </div>

        <!-- Kalender Kerja Judul -->
        <div class="calendar-header">
            KALENDER KERJA DWIBULAN PENGURUS
        </div>

        <!-- Button untuk memilih kalender kerja -->
        <div class="button-container">
            <button onclick="loadDwibulan(1)">Dwibulan 1</button>
            <button onclick="loadDwibulan(2)">Dwibulan 2</button>
            <button onclick="loadDwibulan(3)">Dwibulan 3</button>
            <button onclick="loadDwibulan(4)">Dwibulan 4</button>
            <button onclick="loadDwibulan(5)">Dwibulan 5</button>
            <button onclick="loadDwibulan(6)">Dwibulan 6</button>
        </div>

        <!-- Button untuk memilih bidang -->
        <div class="button-container-bidang" id="button-container-bidang">
            <button onclick="loadBidang('Kalender Kerja Semua Bidang', 1)">Kalender Kerja Semua Bidang</button>
            <button onclick="loadBidang('BP Penginjilan', 1)">BP Penginjilan</button>
            <button onclick="loadBidang('BP Pembinaan', 1)">BP Pembinaan</button>
            <button onclick="loadBidang('BP DOPER', 1)">BP DOPER</button>
            <button onclick="loadBidang('BP Peribadatan', 1)">BP Peribadatan</button>
            <button onclick="loadBidang('BP MULPLIKOM', 1)">BP MULPLIKOM</button>
            <button onclick="loadBidang('BP PERDANA', 1)">BP PERDANA</button>
            <button onclick="loadBidang('Non Bidang', 1)">Non Bidang</button>
        </div>

        <!-- Tempat untuk menampilkan PDF -->
        <div id="pdfViewer">
            <div id="pdfViewer"></div>
        </div>

    </div>

    <div class="music-box">
        <h2>FAST</h2>
        <p>UPK Kr. UNSRAT</p>
        <div class="cover-circle"></div>
        <div class="time-container">
          <span id="start-time">00:00</span>
          <span id="end-time">00:00</span>
        </div>
        <div class="progress-container">
            <div class="progress-bar" id="progress-bar"></div>
          </div>
          <div class="controls">
            <button class="control-btn" id="rewind-btn">⏪</button>
            <button class="control-btn" id="play-btn">▶️</button>
            <button class="control-btn" id="forward-btn">⏩</button>
          </div>
    <script>

const audio = new Audio('FAST.mp3');
    const playBtn = document.getElementById('play-btn');
    const rewindBtn = document.getElementById('rewind-btn');
    const forwardBtn = document.getElementById('forward-btn');
    const progressBar = document.getElementById('progress-bar');
    const startTime = document.getElementById('start-time');
    const endTime = document.getElementById('end-time');

    playBtn.onclick = () => {
      if (audio.paused) {
        audio.play();
        playBtn.textContent = '⏸️';
      } else {
        audio.pause();
        playBtn.textContent = '▶️';
      }
    };

    rewindBtn.onclick = () => {
      audio.currentTime -= 10;
    };

    forwardBtn.onclick = () => {
      audio.currentTime += 10;
    };

    audio.ontimeupdate = () => {
      const progress = (audio.currentTime / audio.duration) * 100;
      progressBar.style.width = `${progress}%`;

      const currentMinutes = Math.floor(audio.currentTime / 60);
      const currentSeconds = Math.floor(audio.currentTime % 60);
      startTime.textContent = `${currentMinutes}:${currentSeconds < 10 ? '0' : ''}${currentSeconds}`;

      const durationMinutes = Math.floor(audio.duration / 60);
      const durationSeconds = Math.floor(audio.duration % 60);
      endTime.textContent = `${durationMinutes}:${durationSeconds < 10 ? '0' : ''}${durationSeconds}`;
    };

        // Mapping PDF untuk setiap dwibulan dan bidang
        const dwibulanProgramPDFs = {
            1: {
                umum: 'umum I.pdf',
                'BP Penginjilan': 'BP PI I.pdf',
                'BP Pembinaan': 'BP PA I.pdf',
                'BP DOPER': 'BP DOPER I.pdf',
                'BP Peribadatan': 'BP PERI I.pdf',
                'BP MULPLIKOM': 'BP MULPLIKOM I.pdf',
                'BP PERDANA': 'BP PERDANA I.pdf',
                'Non Bidang': 'NB I.pdf'
            },
            2: {
                umum: 'DWIBULAN_2_umum.pdf',
                'BP Penginjilan': 'DWIBULAN_2_BP_Penginjilan.pdf',
                'BP Pembinaan': 'DWIBULAN_2_BP_Pembinaan.pdf',
                'BP DOPER': 'DWIBULAN_2_BP_DOPER.pdf',
                'BP Peribadatan': 'DWIBULAN_2_BP_Peribadatan.pdf',
                'BP MULPLIKOM': 'DWIBULAN_2_BP_MULPLIKOM.pdf',
                'BP PERDANA': 'DWIBULAN_2_BP_PERDANA.pdf',
                'Non Bidang': 'DWIBULAN_2_Non_Bidang.pdf'
            },
            3: {
                umum: 'DWIBULAN_3_umum.pdf',
                'BP Penginjilan': 'DWIBULAN_3_BP_Penginjilan.pdf',
                'BP Pembinaan': 'DWIBULAN_3_BP_Pembinaan.pdf',
                'BP DOPER': 'DWIBULAN_3_BP_DOPER.pdf',
                'BP Peribadatan': 'DWIBULAN_3_BP_Peribadatan.pdf',
                'BP MULPLIKOM': 'DWIBULAN_3_BP_MULPLIKOM.pdf',
                'BP PERDANA': 'DWIBULAN_3_BP_PERDANA.pdf',
                'Non Bidang': 'DWIBULAN_3_Non_Bidang.pdf'
            },
            4: {
                umum: 'DWIBULAN_4_umum.pdf',
                'BP Penginjilan': 'DWIBULAN_4_BP_Penginjilan.pdf',
                'BP Pembinaan': 'DWIBULAN_4_BP_Pembinaan.pdf',
                'BP DOPER': 'DWIBULAN_4_BP_DOPER.pdf',
                'BP Peribadatan': 'DWIBULAN_4_BP_Peribadatan.pdf',
                'BP MULPLIKOM': 'DWIBULAN_4_BP_MULPLIKOM.pdf',
                'BP PERDANA': 'DWIBULAN_4_BP_PERDANA.pdf',
                'Non Bidang': 'DWIBULAN_4_Non_Bidang.pdf'
            },
            5: {
                umum: 'DWIBULAN_5_umum.pdf',
                'BP Penginjilan': 'DWIBULAN_5_BP_Penginjilan.pdf',
                'BP Pembinaan': 'DWIBULAN_5_BP_Pembinaan.pdf',
                'BP DOPER': 'DWIBULAN_5_BP_DOPER.pdf',
                'BP Peribadatan': 'DWIBULAN_5_BP_Peribadatan.pdf',
                'BP MULPLIKOM': 'DWIBULAN_5_BP_MULPLIKOM.pdf',
                'BP PERDANA': 'DWIBULAN_5_BP_PERDANA.pdf',
                'Non Bidang': 'DWIBULAN_5_Non_Bidang.pdf'
            },
            6: {
                umum: 'DWIBULAN_6_umum.pdf',
                'BP Penginjilan': 'DWIBULAN_6_BP_Penginjilan.pdf',
                'BP Pembinaan': 'DWIBULAN_6_BP_Pembinaan.pdf',
                'BP DOPER': 'DWIBULAN_6_BP_DOPER.pdf',
                'BP Peribadatan': 'DWIBULAN_6_BP_Peribadatan.pdf',
                'BP MULPLIKOM': 'DWIBULAN_6_BP_MULPLIKOM.pdf',
                'BP PERDANA': 'DWIBULAN_6_BP_PERDANA.pdf',
                'Non Bidang': 'DWIBULAN_6_Non_Bidang.pdf'
            }
        };

        // Menampilkan tombol bidang setelah memilih dwibulan
        function loadDwibulan(dwibulanNumber) {
            const buttonContainer = document.getElementById('button-container-bidang');
            buttonContainer.style.display = 'flex';
            // Mengupdate tombol bidang sesuai dwibulan yang dipilih
            document.getElementById('button-container-bidang').innerHTML = `
                <button onclick="loadBidang('Kalender Kerja Semua Bidang', ${dwibulanNumber})">Kalender Kerja Semua Bidang</button>
                <button onclick="loadBidang('BP Penginjilan', ${dwibulanNumber})">BP Penginjilan</button>
                <button onclick="loadBidang('BP Pembinaan', ${dwibulanNumber})">BP Pembinaan</button>
                <button onclick="loadBidang('BP DOPER', ${dwibulanNumber})">BP DOPER</button>
                <button onclick="loadBidang('BP Peribadatan', ${dwibulanNumber})">BP Peribadatan</button>
                <button onclick="loadBidang('BP MULPLIKOM', ${dwibulanNumber})">BP MULPLIKOM</button>
                <button onclick="loadBidang('BP PERDANA', ${dwibulanNumber})">BP PERDANA</button>
                <button onclick="loadBidang('Non Bidang', ${dwibulanNumber})">Non Bidang</button>
            `;
        }

         // Menampilkan tombol bidang setelah memilih dwibulan
    function loadDwibulan(dwibulanNumber) {
        const buttonContainer = document.getElementById('button-container-bidang');
        buttonContainer.style.display = 'flex';
        buttonContainer.innerHTML = ''; // Reset tombol bidang

        const bidangList = Object.keys(dwibulanProgramPDFs[dwibulanNumber]);
        const color = bidangColors[dwibulanNumber]; // Ambil warna sesuai dwibulan

        bidangList.forEach(bidang => {
            const button = document.createElement('button');
            button.textContent = bidang;
            button.style.background = color; // Terapkan warna tombol
            button.onclick = () => loadBidang(bidang, dwibulanNumber);
            buttonContainer.appendChild(button);
        });
    }

    // Fungsi loadBidang untuk menampilkan PDF
    function loadBidang(bidang, dwibulanNumber) {
        const pdfPath = dwibulanProgramPDFs[dwibulanNumber][bidang];

        if (pdfPath) {
            loadPDF(pdfPath); // Menampilkan PDF jika file ada
            hideButtons();    // Menyembunyikan tombol bidang setelah PDF ditampilkan
        } else {
            showNotification(); // Menampilkan notifikasi jika PDF tidak ada
        }
    }

    // Menampilkan PDF ke dalam elemen
    function loadPDF(pdfPath) {
        const pdfViewer = document.getElementById('pdfViewer');
        pdfViewer.innerHTML = `<embed src="${pdfPath}" type="application/pdf" width="100%" height="600px">`;  // Menyesuaikan ukuran PDF
    }

    // Menyembunyikan tombol bidang setelah memilih bidang
    function hideButtons() {
        const buttonContainer = document.getElementById('button-container-bidang');
        buttonContainer.style.display = 'none';
    }

    // Menampilkan box notifikasi saat file PDF belum tersedia
    function showNotification() {
        const pdfViewer = document.getElementById('pdfViewer');
        pdfViewer.innerHTML = `
            <div class="notification-box">
                Untuk file ini belum tersedia. <span>Mohon tunggu, akan tersedia dalam waktu dekat.</span>
            </div>
        `;
    }

    // Warna gradasi untuk tiap dwibulan
    const bidangColors = {
    1: 'linear-gradient(135deg, #E5CEE8, #A1C9FF)', // Lilac to soft blue for Dwibulan 1
    2: 'linear-gradient(135deg, #F1D6F5, #FFB6C1)', // Light lilac to soft pink for Dwibulan 2
    3: 'linear-gradient(135deg, #C5A0D8, #00BFA6)', // Muted lilac to turquoise for Dwibulan 3
    4: 'linear-gradient(135deg, #D1A6D3, #536DFE)', // Warm lilac to royal blue for Dwibulan 4
    5: 'linear-gradient(135deg, #E5CEE8, #FF7043)', // Lilac to muted coral for Dwibulan 5
    6: 'linear-gradient(135deg, #E5CEE8, #607D8B)', // Lilac to slate gray for Dwibulan 6
};



</script>
</body>
</html>
