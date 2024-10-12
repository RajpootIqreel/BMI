# BMI
import React, { useState } from "react";
import {
  StyleSheet,
  Text,
  View,
  TextInput,
  Button,
  TouchableOpacity,
} from "react-native";

export default function App() {
  const [weight, setWeight] = useState("");
  const [height, setHeight] = useState("");
  const [bmi, setBmi] = useState(null);
  const [bmiMessage, setBmiMessage] = useState("");

  // Function to calculate BMI
  const calculateBMI = () => {
    const weightInKg = parseFloat(weight);
    const heightInMeters = parseFloat(height) / 100; // Convert height to meters

    if (
      isNaN(weightInKg) ||
      isNaN(heightInMeters) ||
      weightInKg <= 0 ||
      heightInMeters <= 0
    ) {
      alert("Please enter valid values for height and weight.");
      return;
    }

    const bmiValue = weightInKg / (heightInMeters * heightInMeters);
    setBmi(bmiValue.toFixed(1));
    determineBMICategory(bmiValue);
  };

  // Function to determine the BMI category based on the BMI value
  const determineBMICategory = (bmiValue) => {
    if (bmiValue < 18.5) {
      setBmiMessage("Underweight");
    } else if (bmiValue >= 18.5 && bmiValue <= 24.9) {
      setBmiMessage("Normal weight");
    } else if (bmiValue >= 25 && bmiValue <= 29.9) {
      setBmiMessage("Overweight");
    } else {
      setBmiMessage("Obese");
    }
  };

  // Function to clear the input fields and reset the BMI state
  const clearInputs = () => {
    setWeight("");
    setHeight("");
    setBmi(null);
    setBmiMessage("");
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>BMI Calculator</Text>

      <TextInput
        style={styles.input}
        placeholder="Enter weight in kg"
        keyboardType="numeric"
        value={weight}
        onChangeText={(value) => setWeight(value)}
      />
      <TextInput
        style={styles.input}
        placeholder="Enter height in cm"
        keyboardType="numeric"
        value={height}
        onChangeText={(value) => setHeight(value)}
      />

      <View style={styles.buttonContainer}>
        <Button title="Calculate BMI" onPress={calculateBMI} />
        <TouchableOpacity style={styles.clearButton} onPress={clearInputs}>
          <Text style={styles.clearButtonText}>Clear</Text>
        </TouchableOpacity>
      </View>

      {bmi && (
        <View style={styles.resultContainer}>
          <Text style={styles.resultText}>Your BMI: {bmi}</Text>
          <Text style={styles.resultText}>{bmiMessage}</Text>
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
    padding: 20,
  },
  title: {
    fontSize: 24,
    fontWeight: "bold",
    marginBottom: 20,
  },
  input: {
    height: 40,
    borderColor: "gray",
    borderWidth: 1,
    marginBottom: 15,
    width: "100%",
    paddingLeft: 10,
    borderRadius: 5,
  },
  buttonContainer: {
    flexDirection: "row",
    justifyContent: "space-between",
    width: "100%",
    marginBottom: 20,
  },
  clearButton: {
    backgroundColor: "#f44336",
    padding: 10,
    borderRadius: 5,
    marginLeft: 10,
  },
  clearButtonText: {
    color: "white",
    fontWeight: "bold",
    textAlign: "center",
  },
  resultContainer: {
    marginTop: 20,
    alignItems: "center",
  },
  resultText: {
    fontSize: 18,
    fontWeight: "bold",
    marginVertical: 5,
  },
});
