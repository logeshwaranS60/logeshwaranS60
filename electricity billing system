import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.HashMap;
import java.util.Map;

class Customer {
    private String name;
    private int meterNumber;
    private double previousReading;
    private double currentReading;

    public Customer(String name, int meterNumber) {
        this.name = name;
        this.meterNumber = meterNumber;
        this.previousReading = 0;
        this.currentReading = 0;
    }

    public String getName() {
        return name;
    }

    public int getMeterNumber() {
        return meterNumber;
    }

    public double getPreviousReading() {
        return previousReading;
    }

    public double getCurrentReading() {
        return currentReading;
    }

    public void updateReading(double newReading) {
        this.previousReading = this.currentReading;
        this.currentReading = newReading;
    }

    public double calculateBill(double ratePerUnit) {
        double unitsConsumed = this.currentReading - this.previousReading;
        return unitsConsumed * ratePerUnit;
    }
}

class AdminPanel {
    private Map<Integer, Customer> customers;
    private double ratePerUnit;

    public AdminPanel(double ratePerUnit) {
        this.customers = new HashMap<>();
        this.ratePerUnit = ratePerUnit;
    }

    public String addCustomer(String name, int meterNumber) {
        if (!customers.containsKey(meterNumber)) {
            customers.put(meterNumber, new Customer(name, meterNumber));
            return "Customer added successfully!";
        } else {
            return "A customer with this meter number already exists.";
        }
    }

    public String updateFixedRate(double newRate) {
        this.ratePerUnit = newRate;
        return "Rate per unit updated successfully!";
    }

    public String generateBill(int meterNumber) {
        if (customers.containsKey(meterNumber)) {
            Customer customer = customers.get(meterNumber);
            double bill = customer.calculateBill(ratePerUnit);
            return "Electricity Bill\n" +
                    "Name: " + customer.getName() + "\n" +
                    "Meter Number: " + customer.getMeterNumber() + "\n" +
                    "Previous Reading: " + customer.getPreviousReading() + " kWh\n" +
                    "Current Reading: " + customer.getCurrentReading() + " kWh\n" +
                    "Total Bill: $" + bill;
        } else {
            return "Customer not found.";
        }
    }

    public String updateReading(int meterNumber, double newReading) {
        if (customers.containsKey(meterNumber)) {
            Customer customer = customers.get(meterNumber);
            customer.updateReading(newReading);
            return "Meter reading updated successfully!";
        } else {
            return "Customer not found.";
        }
    }

    public String displayCustomers() {
        if (customers.isEmpty()) {
            return "No customers to display.";
        } else {
            StringBuilder customerList = new StringBuilder("Customer List:\n");
            for (Customer customer : customers.values()) {
                customerList.append("Name: ").append(customer.getName())
                        .append(", Meter Number: ").append(customer.getMeterNumber()).append("\n");
            }
            return customerList.toString();
        }
    }
}

public class ElectricityBillingSystemSwing {
    private JFrame frame;
    private AdminPanel adminPanel;
    private JTextField nameField, meterField, readingField, rateField;
    private JTextArea outputArea;

    public ElectricityBillingSystemSwing() {
        adminPanel = new AdminPanel(0.15); // Default rate per unit
        frame = new JFrame("Electricity Billing System");

        // Layout
        frame.setLayout(new GridLayout(8, 2, 5, 5));

        // Input Fields
        frame.add(new JLabel("Customer Name:"));
        nameField = new JTextField();
        frame.add(nameField);

        frame.add(new JLabel("Meter Number:"));
        meterField = new JTextField();
        frame.add(meterField);

        frame.add(new JLabel("New Reading (kWh):"));
        readingField = new JTextField();
        frame.add(readingField);

        frame.add(new JLabel("Rate per Unit ($):"));
        rateField = new JTextField();
        frame.add(rateField);

        // Buttons
        JButton addCustomerButton = new JButton("Add Customer");
        addCustomerButton.addActionListener(e -> addCustomer());
        frame.add(addCustomerButton);

        JButton updateRateButton = new JButton("Update Rate");
        updateRateButton.addActionListener(e -> updateRate());
        frame.add(updateRateButton);

        JButton updateReadingButton = new JButton("Update Reading");
        updateReadingButton.addActionListener(e -> updateReading());
        frame.add(updateReadingButton);

        JButton generateBillButton = new JButton("Generate Bill");
        generateBillButton.addActionListener(e -> generateBill());
        frame.add(generateBillButton);

        JButton displayCustomersButton = new JButton("Display Customers");
        displayCustomersButton.addActionListener(e -> displayCustomers());
        frame.add(displayCustomersButton);

        JButton clearButton = new JButton("Clear");
        clearButton.addActionListener(e -> clearFields());
        frame.add(clearButton);

        JButton exitButton = new JButton("Exit");
        exitButton.addActionListener(e -> System.exit(0));
        frame.add(exitButton);

        // Output Area
        outputArea = new JTextArea(10, 30);
        outputArea.setEditable(false);
        frame.add(new JScrollPane(outputArea));

        // Final Frame Setup
        frame.setSize(500, 400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    private void addCustomer() {
        String name = nameField.getText();
        int meterNumber = Integer.parseInt(meterField.getText());
        String result = adminPanel.addCustomer(name, meterNumber);
        outputArea.setText(result);
    }

    private void updateRate() {
        double rate = Double.parseDouble(rateField.getText());
        String result = adminPanel.updateFixedRate(rate);
        outputArea.setText(result);
    }

    private void updateReading() {
        int meterNumber = Integer.parseInt(meterField.getText());
        double reading = Double.parseDouble(readingField.getText());
        String result = adminPanel.updateReading(meterNumber, reading);
        outputArea.setText(result);
    }

    private void generateBill() {
        int meterNumber = Integer.parseInt(meterField.getText());
        String result = adminPanel.generateBill(meterNumber);
        outputArea.setText(result);
    }

    private void displayCustomers() {
        String result = adminPanel.displayCustomers();
        outputArea.setText(result);
    }

    private void clearFields() {
        nameField.setText("");
        meterField.setText("");
        readingField.setText("");
        rateField.setText("");
        outputArea.setText("");
    }

    public static void main(String[] args) {
        new ElectricityBillingSystemSwing();
    }
}
