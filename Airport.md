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
