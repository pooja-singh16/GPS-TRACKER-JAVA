import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URI;
import java.net.URL;

public class Main extends JFrame {

    private JLabel latValue, lonValue, cityValue, countryValue;
    private JButton getLocationBtn, openMapBtn;

    private String latitude = "";
    private String longitude = "";

    public Main() {

        setTitle("Modern GPS Tracker");
        setSize(450, 350);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout());

        // Background Panel
        JPanel background = new JPanel();
        background.setBackground(new Color(30, 32, 40));
        background.setLayout(new GridBagLayout());

        // Card Panel
        JPanel card = new JPanel();
        card.setPreferredSize(new Dimension(350, 250));
        card.setBackground(new Color(45, 48, 60));
        card.setLayout(new GridLayout(6, 1, 10, 10));
        card.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));

        JLabel title = new JLabel("📍 GPS Tracker", JLabel.CENTER);
        title.setForeground(Color.WHITE);
        title.setFont(new Font("Arial", Font.BOLD, 20));

        latValue = createLabel("Latitude: -");
        lonValue = createLabel("Longitude: -");
        cityValue = createLabel("City: -");
        countryValue = createLabel("Country: -");

        getLocationBtn = createButton("Get Location");
        openMapBtn = createButton("Open in Google Maps");

        card.add(title);
        card.add(latValue);
        card.add(lonValue);
        card.add(cityValue);
        card.add(countryValue);
        card.add(getLocationBtn);
        card.add(openMapBtn);

        background.add(card);
        add(background);

        // Button Actions
        getLocationBtn.addActionListener(e -> getLocation());
        openMapBtn.addActionListener(e -> openGoogleMaps());
    }

    private JLabel createLabel(String text) {
        JLabel label = new JLabel(text);
        label.setForeground(Color.WHITE);
        label.setFont(new Font("Segoe UI", Font.PLAIN, 14));
        return label;
    }

    private JButton createButton(String text) {
        JButton button = new JButton(text);
        button.setFocusPainted(false);
        button.setBackground(new Color(0, 120, 215));
        button.setForeground(Color.WHITE);
        button.setFont(new Font("Segoe UI", Font.BOLD, 14));
        button.setCursor(new Cursor(Cursor.HAND_CURSOR));
        return button;
    }

    private void getLocation() {
        try {
            URL url = new URL("http://ip-api.com/json");
            HttpURLConnection con = (HttpURLConnection) url.openConnection();
            con.setRequestMethod("GET");

            BufferedReader in = new BufferedReader(
                    new InputStreamReader(con.getInputStream()));

            String inputLine;
            StringBuilder response = new StringBuilder();

            while ((inputLine = in.readLine()) != null) {
                response.append(inputLine);
            }
            in.close();

            String result = response.toString();

            latitude = result.split("\"lat\":")[1].split(",")[0];
            longitude = result.split("\"lon\":")[1].split(",")[0];
            String city = result.split("\"city\":\"")[1].split("\"")[0];
            String country = result.split("\"country\":\"")[1].split("\"")[0];

            latValue.setText("Latitude: " + latitude);
            lonValue.setText("Longitude: " + longitude);
            cityValue.setText("City: " + city);
            countryValue.setText("Country: " + country);

        } catch (Exception e) {
            JOptionPane.showMessageDialog(this,
                    "Error fetching location!",
                    "Error",
                    JOptionPane.ERROR_MESSAGE);
        }
    }

    private void openGoogleMaps() {
        try {
            if (!latitude.isEmpty()) {
                String url = "https://www.google.com/maps?q=" + latitude + "," + longitude;
                Desktop.getDesktop().browse(new URI(url));
            } else {
                JOptionPane.showMessageDialog(this,
                        "Click Get Location First!");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            new Main().setVisible(true);
        });
    }
}