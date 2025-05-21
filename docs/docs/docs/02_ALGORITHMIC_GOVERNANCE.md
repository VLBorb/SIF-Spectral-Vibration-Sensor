# SIF Algorithmic Governance

The Spectral Inhabitation Framework (SIF) governs the sensor’s operation through a defined sequence of algorithmic steps. This pipeline ensures that raw vibration data is transformed into actionable insights and alerts.

The primary steps are:

1.  **Signal Sampling:**
    * Micro-vibrations are captured by the passive piezoelectric transducer.
    * The analog signal is converted to a digital signal by an Analog-to-Digital Converter (ADC).
    * Sampling rates vary by SIF class (e.g., 40-80 kHz) to capture the relevant frequency spectrum[cite: 379]. ADC resolution also varies (12-bit for Low-Budget, 16-bit for Medium-Budget, 24-bit for High-End)[cite: 379, 386, 394, 404].

2.  **Fast Fourier Transform (FFT):**
    * The digitized time-domain signal $x(n)$ is converted into the frequency domain $X(f)$ to analyze its spectral components[cite: 380].
    * Conceptual Formula: $X(f) = \sum_{n=0}^{N-1} x(n)e^{-j2\pi fn/N}$[cite: 380].

3.  **Fractal Transform (DSFT Application):**
    * The frequency-domain signal $X(f)$ is processed using the Dual Spectral Fractmergence Theorem (DSFT).
    * **SASF² (Spectral Adaptive Selective Fractal Feedback)** is applied to amplify coherent patterns[cite: 380].
        * Example Formula: $F_{SASF^2}(f) = \frac{\log(|X(f)| + \epsilon)}{\log(f + \epsilon)} \cdot \exp\left(-\frac{\log(|X(f)| + \epsilon)}{C}\right)$[cite: 380].
    * **DASF² (Dissipative Adaptive Selective Fractal Feedback)** is applied (primarily in Medium and High-End classes) to suppress noise and irrelevant components[cite: 381].
        * Example Formula: $F_{DASF^2}(f) = \frac{\log(|X(f)| + \epsilon)}{\log(f + \epsilon)} \cdot \begin{cases} 0.1 & \text{if } |\log(|X(f)|+\epsilon) - \mu| > D \\ 1 & \text{otherwise} \end{cases}$[cite: 381].
    * $\epsilon$ is a small constant to prevent log(0), $C$ is a coherence threshold, $D$ is a dissipation threshold, and $\mu$ is a measure of central tendency of the log-magnitudes.

4.  **Spectral Divergence Calculation:**
    * The transformed current spectral fingerprint ($F_{DSFT_{current}}(f)$) is compared against a stored baseline fingerprint ($F_{DSFT_{baseline}}(f)$)[cite: 381].
    * Divergence Formula: $Divergence(f) = |F_{DSFT_{baseline}}(f) - F_{DSFT_{current}}(f)|$[cite: 381].

5.  **Key Performance Metrics Calculation:**
    The system calculates several metrics to provide a comprehensive assessment of the equipment's vibrational health:
    * **Spectral Divergence Index (SDI):** The mean of the spectral divergence values across the frequency spectrum. A primary indicator of change.
    * **Root Mean Square Error (RMSE):** Quantifies the time-domain error between current and baseline signals: $\sqrt{\frac{1}{N}\sum_{n=0}^{N-1}(x_{current}(n) - x_{baseline}(n))^2}$[cite: 382].
    * **Dominant Frequency Shift (DFS):** Detects changes in the main operating frequencies by comparing peak frequencies in the baseline and current FFTs[cite: 382].
    * **Signal-to-Noise Ratio (SNR):** Assesses the quality of the signal: $10\log_{10}\left(\frac{\text{Signal Power}}{\text{Noise Power}}\right)$[cite: 383].
    * **Confidence Interval (CI):** Provides statistical reliability for the SDI: $1.96 \cdot \frac{\sigma_{SDI}}{\sqrt{N}}$[cite: 383].
    * **Time-to-Collapse (TCE) / Time-to-Failure Estimate:** A heuristic estimate of remaining operational time, potentially based on SDI trends: e.g., $\max\left(0, \frac{1000 - SDI}{SDI+0.001}\right)$[cite: 383].

6.  **Alert Generation:**
    * If key metrics (especially SDI) exceed predefined or dynamically adapted thresholds (e.g., SDI > 500), an alert is triggered[cite: 383].
    * Alerts are typically transmitted via MQTT or other configured communication channels[cite: 349, 389, 397, 406].

7.  **Calibration:**
    * A baseline spectral fingerprint is established during a calibration phase.
    * To maintain the "no moving parts" design, calibration is initiated via a specific vibration pattern (e.g., three sharp taps detected by the piezoelectric sensor itself) rather than a physical button[cite: 384].
    * During calibration, the sensor captures the normal operational vibrations of the machinery, processes this signal through FFT and DSFT, and stores the result as $F_{DSFT_{baseline}}(f)$[cite: 384].
