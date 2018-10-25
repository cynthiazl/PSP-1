# Buscador de Aeropuertos
**Página principal**
```Java
import javax.swing.*;
import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.EventQueue;

import javax.swing.border.EmptyBorder;
import java.awt.Font;
import java.awt.Graphics;
import java.awt.Image;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class PaginaPrincipal extends JFrame {

	private JPanel contentPane;
	private Image imagen;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {

			public void run() {

				try {

					PaginaPrincipal frame = new PaginaPrincipal();
					frame.setVisible(true);

					ImageIcon img = new ImageIcon("avion.jpg");
					frame.setIconImage(img.getImage());
					frame.setResizable(false);

				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	/**
	 * Create the frame.
	 */
	public PaginaPrincipal() {

		setTitle("Página principal de Aeropuertos");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 672, 280);
		contentPane = new JPanel();
		contentPane.setBackground(new Color(250, 208, 251));
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);

		JLabel lbTitulo = new JLabel("Buscador de Aeropuetos");
		lbTitulo.setForeground(Color.WHITE);
		lbTitulo.setHorizontalAlignment(SwingConstants.CENTER);
		lbTitulo.setFont(new Font("Verdana", Font.BOLD, 30));
		lbTitulo.setBounds(0, 48, 665, 25);
		contentPane.add(lbTitulo);

		ImagePanel imagePanel = new ImagePanel(new ImageIcon("aeropuerto.jpg").getImage());
		imagePanel.setBounds(0, 0, 665, 250);
		contentPane.add(imagePanel);

		JButton btnBuscar = new JButton("Buscar");
		btnBuscar.setBounds(289, 136, 86, 23);
		imagePanel.add(btnBuscar);
		btnBuscar.setFont(new Font("Georgia", Font.PLAIN, 16));
		btnBuscar.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				Buscador nombre = new Buscador();
				nombre.setVisible(true);

			}
		});

	}

}

class ImagePanel extends JPanel {
	private Image img;

	public ImagePanel(Image img) {

		this.img = img;
		Dimension size = new Dimension(img.getWidth(null), img.getHeight(null));

		setPreferredSize(size);
		setMinimumSize(size);
		setMaximumSize(size);
		setSize(size);
		setLayout(null);
	}

	public void paintComponent(Graphics g) {
		g.drawImage(img, 0, 0, null);
	}
}
```
**Clase Airport**
```Java

public class Airport {

	private int id;
	private String code;
	private String name;
	private String city;
	private String country;
	private double latitude;
	private double longitude;
	
	public Airport(int id, String code, String name, String city, String country, double latitude, double longitude) {
		
		this.id = id;
		this.code = code;
		this.name = name;
		this.city = city;
		this.country = country;
		this.latitude = latitude;
		this.longitude = longitude;
	}
	
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getCode() {
		return code;
	}
	public void setCode(String code) {
		this.code = code;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getCity() {
		return city;
	}
	public void setCity(String city) {
		this.city = city;
	}
	public String getCountry() {
		return country;
	}
	public void setCountry(String country) {
		this.country = country;
	}
	public double getLatitude() {
		return latitude;
	}
	public void setLatitude(double latitude) {
		this.latitude = latitude;
	}
	public double getLongitude() {
		return longitude;
	}
	public void setLongitude(double longitude) {
		this.longitude = longitude;
	}
	public String ToString() {
		return "Aeropuerto " + this.name + " ciudad " + this.city + " país " + this.country + " Cod " + this.code;
	}
	
}
```
**Buscador**
```Java
import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Desktop;
import java.awt.EventQueue;
import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.Console;
import java.net.URI;
import java.util.ArrayList;

import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.EmptyBorder;
import javax.swing.table.DefaultTableModel;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JTextField;
import javax.swing.DefaultListModel;
import javax.swing.JButton;
import javax.swing.JList;
import javax.swing.JTable;
import javax.swing.JComboBox;

public class Buscador extends JFrame {

	private String nomAirport = "";

	private JPanel contentPane;
	private JTextField textAeropuerto;
	private JButton btnBuscar;
	private JTable table;
	private JButton btnMapa;

	/**
	 * Launch the application.
	 */
	public static void main(String[] args) {
		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					Buscador frame = new Buscador();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});
	}

	/**
	 * Create the frame.
	 */
	public Buscador() {

		LeoFichero leeFichero = new LeoFichero();
		ArrayList<Airport> airports = leeFichero.Lee();

		setTitle("Buscador de Aeropuertos");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 630, 500);
		contentPane = new JPanel();
		contentPane.setBackground(new Color(250, 208, 251));
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		contentPane.setLayout(null);

		JLabel lbTituloBuscador = new JLabel("Buscar Aeropuerto");
		lbTituloBuscador.setBounds(220, 48, 170, 25);
		contentPane.add(lbTituloBuscador);
		lbTituloBuscador.setFont(new Font("Verdana", Font.PLAIN, 18));

		contentPane.add(lbTituloBuscador);

		JLabel lblIntroduzcaElNombre = new JLabel("Introduzca Ciudad, País o Cod Aeropuerto:");
		lblIntroduzcaElNombre.setFont(new Font("Verdana", Font.PLAIN, 14));
		lblIntroduzcaElNombre.setBounds(10, 129, 304, 14);
		contentPane.add(lblIntroduzcaElNombre);

		JLabel informo = new JLabel("");
		informo.setForeground(Color.RED);
		informo.setBounds(324, 128, 270, 20);
		contentPane.add(informo);
	
		// Recojo el texto
		textAeropuerto = new JTextField();
		textAeropuerto.setBounds(324, 128, 270, 20);
		contentPane.add(textAeropuerto);
		textAeropuerto.setColumns(10);

		JComboBox comboBoxResultado = new JComboBox();
		comboBoxResultado.setBounds(131, 270, 310, 20);
		contentPane.add(comboBoxResultado);

		btnMapa = new JButton("Mapa");
		btnMapa.setBounds(246, 353, 89, 23);
		contentPane.add(btnMapa);
		btnMapa.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent e) {
				// TODO Auto-generated method stub
				if (textAeropuerto.getText().isEmpty()) {

					informo.setText("Debe introducir texto");

				} else {

					Desktop browser = Desktop.getDesktop();
					String url = "https://www.google.com/maps/place/{name}/@{latitude},{longitude},15z/data=!3m1!4b1!4m5!3m4!1s0x0:0x0!8m2!3d38.2821999!4d-0.558156?hl=es";

					for (Airport aeropuerto : airports) {

						if (comboBoxResultado.getSelectedItem().equals(aeropuerto.getName().replace("\"", ""))) {
							
							try {
								
								url = url.replace("{name}", aeropuerto.getName().replace("\"", "").replaceAll(" ", "+"));
								url = url.replace("{latitude}", Double.toString(aeropuerto.getLatitude()));
								url = url.replace("{longitude}", Double.toString(aeropuerto.getLongitude()));
								
								browser.browse(new URI(url));
								
								System.out.println(url);

							} catch (Exception e2) {
								// TODO: handle exception
								JOptionPane.showMessageDialog(null, "Ha ocurrido un error insesperado: " + e2.getMessage());
							}
						}
					}
				}
			}
		});

		// Boton para buscar el aeropuerto
		btnBuscar = new JButton("Buscar");
		btnBuscar.setFont(new Font("Georgia", Font.PLAIN, 16));
		btnBuscar.setBounds(246, 162, 89, 23);
		contentPane.add(btnBuscar);

		btnBuscar.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				
				comboBoxResultado.removeAllItems();

				if (textAeropuerto.getText().isEmpty()) {

					JOptionPane.showMessageDialog(null, "Debe introducir texto");

				} else {

					ArrayList<Airport> resultados = new ArrayList<Airport>();

					for (Airport airport : airports) {

						if ((textAeropuerto.getText().length() == 3 && textAeropuerto.getText().toLowerCase().equals(airport.getCode().toLowerCase().replace("\"", "")) || 
							(  airport.getCity().toLowerCase().contains(textAeropuerto.getText().toLowerCase())	|| 
							   airport.getCountry().toLowerCase().contains(textAeropuerto.getText().toLowerCase()) || 
							   airport.getName().toLowerCase().contains(textAeropuerto.getText().toLowerCase())))) {

							resultados.add(airport);
							comboBoxResultado.addItem(airport.getName().replace("\"", ""));
							 //System.out.println("Encontrado" + airport.getCode()+ airport.getName());
						}
					}

				}
			}
		});
	}
}

/*
 * if (!textSeleccionado.getText().equals("")) { String resultado = "", mismoVal
 * = ""; if (textSeleccionado.getText().equals("Buscar")) {
 * 
 * for (int i = 0; i < airports.size(); i++) { if
 * (airports.get(i).toString().toUpperCase()
 * .contains(textSeleccionado.getText().toString().toUpperCase())) { resultado =
 * airports.get(i).toString(); comboBoxResultado.addItem(resultado);
 * 
 * } } btnBuscar.setText("Volver a Buscar");
 * 
 * textSeleccionado.setEditable(false); } else if
 * (btnBuscar.getText().equals("Volver a Buscar")) {
 * comboBoxResultado.removeAllItems(); btnBuscar.setText("Buscar");
 * textSeleccionado.setEditable(true); informo.setText(""); } }
 */
```
**Leer el fichero**
```Java
import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;

import javax.swing.text.AbstractDocument.LeafElement;

public class LeoFichero {

	public ArrayList<Airport> Lee() {

		ArrayList<Airport> airports = new ArrayList<Airport>();
		String leoCSV = ""; 
		
		try {
			File fichero = new File("airports.csv");
			FileReader leer = new FileReader(fichero);
			
			BufferedReader leoLineas = new BufferedReader(leer);
			
			while ((leoCSV = leoLineas.readLine()) != null) {
				String[] datos = leoCSV.split(",(?=([^\"]*\"[^\"]*\")*[^\"]*$)");
				
				//imprime datos
				//System.out.println(datos[6]);
				
				Airport airport = new Airport(Integer.parseInt(datos[0]), datos[4], datos[1], datos[2], datos[3], Double.parseDouble(datos[6]), Double.parseDouble(datos[7]));
				
				airports.add(airport);				
			}
			
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
			
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
		return airports;
	}

}
```


