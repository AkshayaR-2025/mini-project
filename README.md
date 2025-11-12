// Project Name: PatientHealthDashboard
// Package Name: patienthealth
// Class Name: PatientHealthDashboard

package patienthealth;

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class PatientHealthDashboard extends JFrame implements ActionListener {

    // Components
    private JTextField nameField, ageField, heartRateField, temperatureField;
    private JTextArea displayArea;
    private JButton addButton, clearButton;

    public PatientHealthDashboard() {
        setTitle("Patient Health Dashboard");
        setSize(450, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // ----- Input Panel -----
        JPanel inputPanel = new JPanel(new GridLayout(4, 2, 10, 10));

        inputPanel.add(new JLabel("Patient Name:"));
        nameField = new JTextField();
        inputPanel.add(nameField);

        inputPanel.add(new JLabel("Age:"));
        ageField = new JTextField();
        inputPanel.add(ageField);

        inputPanel.add(new JLabel("Heart Rate:"));
        heartRateField = new JTextField();
        inputPanel.add(heartRateField);

        inputPanel.add(new JLabel("Temperature:"));
        temperatureField = new JTextField();
        inputPanel.add(temperatureField);

        add(inputPanel, BorderLayout.NORTH);

        // ----- Buttons -----
        JPanel buttonPanel = new JPanel();
        addButton = new JButton("Add Record");
        clearButton = new JButton("Clear");
        addButton.addActionListener(this);
        clearButton.addActionListener(this);
        buttonPanel.add(addButton);
        buttonPanel.add(clearButton);

        add(buttonPanel, BorderLayout.CENTER);

        // ----- Display Area -----
        displayArea = new JTextArea();
        displayArea.setEditable(false);
        add(new JScrollPane(displayArea), BorderLayout.SOUTH);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == addButton) {
            String name = nameField.getText().trim();
            String age = ageField.getText().trim();
            String heartRate = heartRateField.getText().trim();
            String temperature = temperatureField.getText().trim();

            // Validation
            if (name.isEmpty() || age.isEmpty() || heartRate.isEmpty() || temperature.isEmpty()) {
                JOptionPane.showMessageDialog(this, "Please fill all fields!", "Error", JOptionPane.ERROR_MESSAGE);
                return;
            }

            // Display details
            displayArea.append("Patient Name: " + name + "\n");
            displayArea.append("Age: " + age + "\n");
            displayArea.append("Heart Rate: " + heartRate + " bpm\n");
            displayArea.append("Temperature: " + temperature + " °C\n");
            displayArea.append("--------------------------------------\n");

            // Clear input fields after adding
            nameField.setText("");
            ageField.setText("");
            heartRateField.setText("");
            temperatureField.setText("");

        } else if (e.getSource() == clearButton) {
            displayArea.setText("");
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            new PatientHealthDashboard().setVisible(true);
        });
    }
}
