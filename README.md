# AI-Driven-VLSI-Circuit-Optimization-Using-Pareto-Optimization
• Optimized CMOS circuit design using AI techniques like Machine Learning (Random Forest) and Genetic Algorithms to balance Power, Performance (Delay), and Area (PPA). • Designed and simulated circuits in LTspice, extracting key metrics for training the model. Automated transistor sizing for efficient VLSI design without manual tuning.

# 🪜 Project Workflow Breakdown
# STEP 1: Data Generation from LTspice
Tool Used: LTspice (for circuit simulation).

Circuits Simulated: CMOS Inverter, NAND gate, pseudo-NMOS NOR gate.

Variables Changed:

NMOS Width (NMOS_W)
PMOS Width (PMOS_W)

Supply Voltage (VDD)

Outputs Extracted:

Power = AVG(I(VDD)) × VDD

Delay = Time difference between 50% input and output transitions

Area = Function of NMOS_W + PMOS_W

Other features: Rise/Fall time, Energy, Noise Margins, etc.

Format: CSV file with each row = one simulation.

# STEP 2: Preprocessing the Data Using Spyder
Load CSV with proper encoding detection.

Normalize input features (NMOS_W, PMOS_W, VDD) using StandardScaler.

Define inputs (X) and targets (y with multiple PPA features).

Split into training and test sets.

# STEP 3: ML Model Training (Neural Network)
Library: TensorFlow/Keras.

Model Structure:

Input: 3 neurons

Hidden Layers: [128, 64, 32] with ReLU activation

Output: 13 neurons for 13 PPA targets

Loss: Mean Squared Error (MSE)

Optimizer: Adam

Callback: Early stopping on validation loss.

Evaluation: Mean Absolute Error (MAE) for each PPA metric.

# STEP 4: Save & Visualize Predictions
Save predicted values (Power, Delay, Area...) to CSV.

Create scatter plots:

Power vs Area

Delay vs Area

Power vs Delay

# STEP 5: Optimization Using KNN + Genetic Algorithm
Why KNN? Simpler and faster to approximate ML predictions for optimization.

Fitness Function:

Takes (NMOS_W, PMOS_W) as input

Uses KNN to predict Power, Delay, Area

Adjusts predictions slightly (e.g., noise in delay to simulate variation)

DEAP Framework used for:

Multi-objective optimization using NSGA-II

Genetic operations: selection, crossover, mutation

Design Priorities Evaluated:

All three (power, delay, area)

Pairwise (delay-power, delay-area, area-power)

Individual (delay only, power only, area only)

Output:

Optimal NMOS_W and PMOS_W for each priority

Power, delay, area values for each

# STEP 6: Visualization of Optimization Results
Radar Plot:

Compare normalized power/delay/area across all priorities

3D Scatter Plot:

Visualize Pareto fronts for each priority

Highlight best solution with a red star
