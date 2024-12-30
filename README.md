# Digital-Signal-Processing-Project
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>README</title>
</head>
<body>
  <h1 align="center">Chirp Signal Analysis: Estimating Room Occupancy</h1>
  
  <h2>Project Objective</h2>
  <p>The primary objective of this project is to utilize chirp signal generation, audio signal processing, and machine learning to estimate the number of people in a room. Chirp signals are sent out, and their reflections are recorded. Using extracted features like amplitude and phase, a model is trained to predict the number of people present in the room based on the characteristics of the reflected signals.</p>

  <h2>Project Files</h2>
  <p>The project contains the following Python files:</p>
  <ol>
    <li>
      <strong>main_comp.py:</strong>
      <ul>
        <li>Contains the main code for running the project and generating outputs for the number of people in the room.</li>
        <li>Includes commented sections with code from earlier versions of the project for reference.</li>
      </ul>
    </li>
    <li><strong>Circular Buffer:</strong> Handles efficient storage and retrieval of recorded audio data in a cyclic manner.</li>
    <li><strong>Digital Filter:</strong> Implements a high-pass filter to reduce noise in audio recordings.</li>
    <li><strong>Signal Processor:</strong> Extracts features like FFT results from audio data and calculates distances for further analysis.</li>
  </ol>

  <h2>Project Workflow</h2>
  <h3>1. Signal Generation and Playback</h3>
  <ul>
    <li><strong>Purpose:</strong> Generate a series of chirp signals, ranging from 16 kHz to 19 kHz, to capture audio reflections from the environment.</li>
    <li><strong>Method:</strong> A linear chirp signal is generated for a duration of 40 ms and repeated 50 times. Each chirp is normalized to ensure consistent amplitude.</li>
    <li><strong>Code Implementation:</strong> The <code>generate_chirps</code> function creates multiple chirps using the <code>chirp</code> function from <code>scipy.signal</code>. Chirps are played back using the <code>sounddevice</code> library.</li>
  </ul>

  <h3>2. Data Collection and Analysis</h3>
  <ul>
    <li><strong>Purpose:</strong> Record and analyze the reflected audio signals to extract features (amplitude and phase).</li>
    <li><strong>Method:</strong>
      <ul>
        <li>The <code>sounddevice</code> library records reflected audio.</li>
        <li>The Short-Time Fourier Transform (STFT) is applied to the recorded audio to compute the frequency domain representation.</li>
        <li>Average amplitude and phase values are extracted from the STFT results.</li>
      </ul>
    </li>
    <li><strong>Code Implementation:</strong> The <code>analyze_chirp</code> function computes the average amplitude and phase of the STFT-transformed audio signals.</li>
  </ul>

  <h3>3. Machine Learning Model</h3>
  <ul>
    <li><strong>Purpose:</strong> Train a Support Vector Classifier (SVC) to predict the number of people in the room based on the extracted features.</li>
    <li><strong>Dataset:</strong> A CSV file (<code>chirp_data.csv</code>) contains labeled data with features (Amplitude, Phase) and the target variable (People).</li>
    <li><strong>Method:</strong>
      <ul>
        <li>Data is split into training (80%) and testing (20%) sets using <code>train_test_split</code>.</li>
        <li>An SVC with an RBF kernel is trained using the training data.</li>
        <li>Model accuracy is evaluated using the test data.</li>
      </ul>
    </li>
    <li><strong>Code Implementation:</strong> The SVC model is trained and tested using the <code>sklearn</code> library, achieving accuracy printed in the output.</li>
  </ul>

  <h3>4. Real-Time Testing</h3>
  <ul>
    <li><strong>Purpose:</strong> Play and record chirps in real-time, analyze the audio, and predict the number of people in the room.</li>
    <li><strong>Method:</strong>
      <ul>
        <li>The <code>generate_chirps</code> function creates chirps, which are played and recorded in a loop.</li>
        <li>Extracted features from recorded audio are fed into the trained SVC model to make predictions.</li>
      </ul>
    </li>
    <li><strong>Code Implementation:</strong>
      <ul>
        <li><code>sd.play</code> and <code>sd.rec</code> are used for real-time playback and recording.</li>
        <li>Average amplitude and phase of recorded signals are computed and passed to the SVC model for prediction.</li>
      </ul>
    </li>
  </ul>

  <h2>Conclusion</h2>
  <p>This project demonstrates the feasibility of using chirp signals, combined with signal processing and machine learning, to estimate the number of people in an enclosed space to be one or more than one. The system provides a foundation for further enhancements, such as improving the model's accuracy, optimizing feature extraction, and expanding real-world applications like occupancy detection or security monitoring.</p>
</body>
</html>
