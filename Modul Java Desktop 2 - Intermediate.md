# Sinau Java Desktop 2 - Intermediate #

## [PERTEMUAN 1] ##

Selamat datang disesi Java Intermediate. Pada kesempatan kali ini kita akan lebih mendalami misteri apa saja yang terdapat didalam pemrograman Java.

## Java Collection Framework ##

Java Collection Framework merupakan standar dari Java untuk menghandle bagaimana pengelompokan object ditata/diatur.

### List ###

List adalah jenis collection yang teratur tetapi tidak terurut. List mempunyai index yang disusun berdasarkan urutan kapan item dimasukkan ke dalam List. Isi dari List bersifat tidak unik, alias dua buah item yang sama bisa dimasukkan berkali kali ke dalam List.

Lihat source code modul `CobaList.java`.

### Map ###

Map adalah bentuk struktur data yang berpasangan antara key-value, yang mana Key merupakan bersifat unik.

Lihat source code modul `CobaMap.java`.

### Set ###

Set adalah collection yang bersifat unik. Set digunakan kalau anda memerlukan collection yang isinya harus unik / tidak boleh sama secara berulang.

Lihat source code modul `CobaSet.java`.


## [PERTEMUAN 2] ##

### Java GUI ###

Untuk membuat aplikasi GUI di Java kita bisa menggunakan library Java Swing.

Untuk memulai seperti biasa kita mulai dengan HelloWorld GUI terlebih dahulu. Pertama kita buat class dengan nama HelloGUI. Supaya class ini dapat mengimplementasikan GUI, maka class yang kita buat ini harus diturunkan dari class JFrame (extends JFrame).

```java
import javax.swing.JFrame;
public class HelloGUI extends JFrame{
	public HelloGUI(){
	}
	public static void main(String[] args){
	}
}
```

Setelah setelah itu, untuk memberikan judul pada Frame kita panggil method setTitle() dan kita berikan parameter judul yang kita inginkan.

```java
import javax.swing.JFrame;
public class HelloGUI extends JFrame{
	public HelloGUI(){
		setTitle("Hello GUI");
	}
	public static void main(String[] args){
	}
}
```

Untuk menentukan lebar dan tinggi Frame kita panggil method setSize().

```java
import javax.swing.JFrame;
public class HelloGUI extends JFrame{
	public HelloGUI(){
		setTitle("Hello GUI");
		setSize(300,300);
	}
	public static void main(String[] args){
	}
}
```

Jangan lupa untuk menambahkan method setDefaultCloseOperation(). Method ini digunakan untuk memberi tahu Frame apa yang harus dilakukan ketika tombol close ditekan.

```java
import javax.swing.JFrame;
public class HelloGUI extends JFrame{
	public HelloGUI(){
		setTitle("Hello GUI");
		setSize(300,300);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	}
	public static void main(String[] args){
	}
}
```

Setelah semuanya siap, untuk menampilkan Frame kita buat instansiasi didalam method main.

```java
import javax.swing.JFrame;
public class HelloGUI extends JFrame{
	public HelloGUI(){
		setTitle("Hello GUI");
		setSize(300,300);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	}
	public static void main(String[] args){
		HelloGUI hello = new HelloGUI();
		hello.setVisible(true);
	}
}
```

### Swing Component ###

Swing menyediakan GUI kompenen yang sangat lengkap yang dapat kita gunakan dengan mudah. Mulai dari button, textfield, textarea sampai table. Sekarang kita akan coba tambahkan komponen ke dalam Frame yang sudah kita buat tadi.

```java
import java.awt.FlowLayout;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JTextField;
public class HelloGUI extends JFrame{
	private JButton button;
	private JTextField textField;
	public HelloGUI(){
		setLayout(new FlowLayout());
		button = new JButton("OK");
		textField = new JTextField(20);
		setTitle("Hello GUI");
		setSize(300,300);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		add(button);
		add(textField);
	}
	public static void main(String[] args){
		HelloGUI hello = new HelloGUI();
		hello.setVisible(true);
	}
}
```

### Event Handling ###

Program yang sudah kita buat diatas hanya menghasilkan sebuah tampilan dan jika button kita tekan masih belum bisa melakukan apapun. Tidaklah bagus rasanya jika kita membuat program tetapi tidak bisa melakukan apapun. Sekarang kita akan tambahkan event handling supaya button yang kita buat dapat melakukan event yang kita inginkan. Misalnya kita berikan event, ketika button ditekan maka judul Frame akan berubah mengikuti tulisan yang terdapat pada TextField.

```java
import java.awt.FlowLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JTextField;
public class HelloGUI extends JFrame{
	private JButton button;
	private JTextField textField;
	public HelloGUI(){
		setLayout(new FlowLayout());
		button = new JButton("OK");
		textField = new JTextField(20);
		setTitle("Hello GUI");
		setSize(300,300);
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		button.addActionListener(new ActionListener(){
			public void actionPerformed(ActionEvent arg0) {
				setTitle(textField.getText());
			}
		});
		add(button);
		add(textField);
	}
	public static void main(String[] args){
		HelloGUI hello = new HelloGUI();
		hello.setVisible(true);
	}
}
```


## [PERTEMUAN 3] ##

Pada pertemuan kali ini kita akan belajar membuat aplikasi GUI dengan konsep MVC.

### Java GUI MVC ###

MVC merupakan sebuah design pattern, kepanjangan dari Model View Controller. Bertujuan untuk memisahkan antara Model, View dan Controller atau membagi beban kerja class. Membagi beban kerja ini akan membuat class yang kita buat memiliki pekerjaan yang lebih spesifik sehingga mudah untuk dimaintain / maintainable, membuat program kita terpisah menjadi bagian yang kecil-kecil sehingga mudah untuk dibaca / readable / understandable, ketergantungan antar komponen juga bisa diminimalisir / loosely couple sehingga setiap ada perubahan pada bagian yang lain tidak akan berpengaruh kebagian yang lain.

### Practice ###

Kita akan mencoba membuat ulang bangundatar (mencari luas segitiga dan persegipanjang) yang dulu pernah kita buat pada modul pertama. Pertama-tama kita buat project baru. Kemudian buat 5 buah package.

```java
javaintermediate.session3 // Untuk menempatkan main class
javaintermediate.session3.bangundatar // Untuk menempatkan class-class model
javaintermediate.session3.action // Untuk menempatkan class-class controller
javaintermediate.session3.gui // Untuk menempatkan class-class view
javaintermediate.session3.common // Untuk menempatkan class-class helper
```

#### Model ####

Kita mulai dari yang paling mudah, kita buat modelnya dulu.

```java
package javaintermediate.session3.bangundatar;

public interface BangunDatar {
	public double hitungLuas();
}
```

Dibawah ini adalah class model untuk segitiga.

```java
package javaintermediate.session3.bangundatar;

public class Segitiga implements BangunDatar {
	private double alas;
	private double tinggi;

	public double getAlas() {
		return alas;
	}
	public void setAlas(double alas) {
		this.alas = alas;
	}
	public double getTinggi() {
		return tinggi;
	}
	public void setTinggi(double tinggi) {
		this.tinggi = tinggi;
	}

	@Override
	public double hitungLuas() {
		return ((alas * tinggi) / 2);
	}
}
```

#### Common ####

Setelah itu kita buat sebuah interface untuk menaruh semua definisi yang akan kita gunakan nanti di class GUI. Interface yang kita buat ini berfungsi seperti kamus yang akan menterjemahkan setiap judul yang digunakan pada class GUI.

```java
package javaintermediate.session3.common;

public interface BangunDatarConstantsDefinition {
	String BUTTON_COMMON_LUAS = "Hitung Luas";

	// Definisi Main Frame
	String FRAME_MAINFRAME_TITLE = "Hitung Luas Bangun Datar";
	String MENU_MAINFRAME_VIEW = "View";
	String MENUITEM_MAINFRAME_VIEW_SEGITIGA = "Luas Segitiga";
	String MENUITEM_MAINFRAME_VIEW_PERSEGIPANJANG = "Luas Persegi Panjang";

	// Definisi segitiga
	String FRAME_SEGITIGA_TITLE = "Hitung Luas Segitiga";
	String LABEL_SEGITIGA_ALAS = "Alas";
	String LABEL_SEGITIGA_TINGGI = "Tinggi";
	String LABEL_SEGITIGA_LUAS = "Luas";

	// Definisi persegi panjang
	String FRAME_PERSEGIPANJANG_TITLE = "Hitung Luas Persegi Panjang";
	String LABEL_PERSEGIPANJANG_PANJANG = "Panjang";
	String LABEL_PERSEGIPANJANG_LEBAR = "Lebar";
	String LABEL_PERSEGIPANJANG_LUAS = "Luas";
}
```

#### GUI / View ####

Pertama kita buat satu buah abstract class yang berfungsi sebagai constructor GUI yang kita buat.

```java
package javaintermediate.session3.gui;

public abstract class AbstractFrameConstructor {
	protected AbstractFrameConstructor() {
		constructGui();
		addFrameComponent();
		addFrameAction();
	}

	protected abstract void constructGui();
	protected abstract void addFrameComponent();
	protected abstract void addFrameAction();

	public abstract void show();
	public abstract void hide();
}
```

Dibawah ini adalah GUI untuk segitiga yang berupa internal frame.

```java
package javaintermediate.session3.gui;

import javax.swing.JButton;
import javax.swing.JInternalFrame;
import javax.swing.JLabel;
import javax.swing.JTextField;

import javaintermediate.session3.action.SegitigaClickListener;
import javaintermediate.session3.common.BangunDatarConstantsDefinition;

public class SegitigaGui extends AbstractFrameConstructor {
	private JInternalFrame segitigaFrame;
	private JLabel alasLabel;
	private JLabel tinggiLabel;
	private JLabel luasLabel;
	private JTextField alasTextField;
	private JTextField tinggiTextField;
	private JTextField luasTextField;
	private JButton luasButton;

	public SegitigaGui() {
		super();
	}

	@Override
	protected void constructGui() {
		segitigaFrame = new JInternalFrame(BangunDatarConstantsDefinition.FRAME_SEGITIGA_TITLE, // title
				true, // resizable
				true, // closable
				true, // maximizable
				true);// iconifiable
		segitigaFrame.setSize(400, 200);
		segitigaFrame.setLayout(null);
		segitigaFrame.setDefaultCloseOperation(JInternalFrame.HIDE_ON_CLOSE);

		alasLabel = new JLabel(BangunDatarConstantsDefinition.LABEL_SEGITIGA_ALAS);
		tinggiLabel = new JLabel(BangunDatarConstantsDefinition.LABEL_SEGITIGA_TINGGI);
		luasLabel = new JLabel(BangunDatarConstantsDefinition.LABEL_SEGITIGA_LUAS);

		alasTextField = new JTextField(20);
		tinggiTextField = new JTextField(20);
		luasTextField = new JTextField(20);

		luasButton = new JButton(BangunDatarConstantsDefinition.BUTTON_COMMON_LUAS);
	}

	@Override
	protected void addFrameComponent() {
		segitigaFrame.add(alasLabel);
		segitigaFrame.add(tinggiLabel);
		segitigaFrame.add(luasLabel);
		segitigaFrame.add(luasButton);
		segitigaFrame.add(alasTextField);
		segitigaFrame.add(tinggiTextField);
		segitigaFrame.add(luasTextField);

		alasLabel.setBounds(10, 10, 100, 20);
		tinggiLabel.setBounds(10, 30, 100, 20);
		luasLabel.setBounds(10, 50, 100, 20);

		alasTextField.setBounds(150, 10, 200, 20);
		tinggiTextField.setBounds(150, 30, 200, 20);
		luasTextField.setBounds(150, 50, 200, 20);

		luasButton.setBounds(150, 70, 200, 20);
	}

	@Override
	protected void addFrameAction() {
		// buka comment ini setelah membuat class action
		// luasButton.addActionListener(new SegitigaClickListener(alasTextField, tinggiTextField, luasTextField));
	}

	public JInternalFrame getSegitigaFrame() {
		return segitigaFrame;
	}

	@Override
	public void show() {
		segitigaFrame.setVisible(true);
	}

	@Override
	public void hide() {
		segitigaFrame.setVisible(false);
	}
}
```

GUI yang berikutnya kita buat untuk tampilan utama aplikasi bangun datar kita.

```java
package javaintermediate.session3.gui;

import java.awt.BorderLayout;

import javax.swing.JDesktopPane;
import javax.swing.JFrame;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;

import javaintermediate.session3.action.MainBangunDatarMenuViewSegitigaClickListener;
import javaintermediate.session3.common.BangunDatarConstantsDefinition;

public class MainBangunDatarGui extends AbstractFrameConstructor {
	private JFrame mainFrame;
	private JDesktopPane mainDesktop;
	private JMenuBar mainMenuBar;
	private JMenu viewMenu;
	private JMenuItem viewMenuItemSegitiga;
	private JMenuItem viewMenuItemPersegiPanjang;

	private SegitigaGui segitigaGui;

	public MainBangunDatarGui() {
		super();
	}

	@Override
	protected void constructGui() {
		segitigaGui = new SegitigaGui();

		// Instansiasi Desktop Pane
		mainDesktop = new JDesktopPane();

		// Instansiasi Menu Bar
		mainMenuBar = new JMenuBar();
		viewMenu = new JMenu(BangunDatarConstantsDefinition.MENU_MAINFRAME_VIEW);
		viewMenuItemSegitiga = new JMenuItem(BangunDatarConstantsDefinition.MENUITEM_MAINFRAME_VIEW_SEGITIGA);
		viewMenuItemPersegiPanjang = new JMenuItem(BangunDatarConstantsDefinition.MENUITEM_MAINFRAME_VIEW_PERSEGIPANJANG);

		// Instansiasi JFrame
		mainFrame = new JFrame(BangunDatarConstantsDefinition.FRAME_MAINFRAME_TITLE);
		mainFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		mainFrame.setSize(500, 300);
	}

	@Override
	protected void addFrameComponent() {
		mainDesktop.add(segitigaGui.getSegitigaFrame());
		mainDesktop.setDragMode(JDesktopPane.OUTLINE_DRAG_MODE);

		viewMenu.add(viewMenuItemSegitiga);
		viewMenu.add(viewMenuItemPersegiPanjang);
		mainMenuBar.add(viewMenu);

		mainFrame.setJMenuBar(mainMenuBar);
		mainFrame.add(mainDesktop, BorderLayout.CENTER);
	}

	@Override
	protected void addFrameAction() {
    	// buka comment ini setelah membuat class action
		// viewMenuItemSegitiga.addActionListener(new MainBangunDatarMenuViewSegitigaClickListener(segitigaGui, null));
	}

	@Override
	public void show() {
		mainFrame.setVisible(true);
	}

	@Override
	public void hide() {
		// do nothing
	}
}
```

#### Action / Controller ####

Setelah kita buat GUI sekarang kita buat actionnya, yang berfungsi untuk memberikan definisi apasaja yang akan dilakukan ketika suatu event terjadi pada GUI.

Dibawah ini merupakan action class untuk segitiga GUI.

```java
package javaintermediate.session3.action;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JTextField;

import org.apache.commons.lang.StringUtils;

import javaintermediate.session3.bangundatar.Segitiga;

public class SegitigaClickListener implements ActionListener {
	private JTextField alasTextField;
	private JTextField tinggiTextField;
	private JTextField luasTextField;

	private Segitiga segitiga;

	public SegitigaClickListener(JTextField alasTextField, JTextField tinggiTextField, JTextField luasTextField) {
		this.alasTextField = alasTextField;
		this.tinggiTextField = tinggiTextField;
		this.luasTextField = luasTextField;

		segitiga = new Segitiga();
	}

	@Override
	public void actionPerformed(ActionEvent arg0) {
		if(StringUtils.isNotEmpty(alasTextField.getText())) {
			segitiga.setAlas(Double.parseDouble(alasTextField.getText()));
		} else {
			segitiga.setAlas(0);
		}

		if(StringUtils.isNotEmpty(tinggiTextField.getText())) {
			segitiga.setTinggi(Double.parseDouble(tinggiTextField.getText()));
		} else {
			segitiga.setTinggi(0);
		}

		luasTextField.setText(segitiga.hitungLuas() + StringUtils.EMPTY);
	}
}
```

Dibawah ini merupakan action class untuk tampilan utama GUI.

```java
package javaintermediate.session3.action;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javaintermediate.session3.gui.AbstractFrameConstructor;

public class MainBangunDatarMenuViewSegitigaClickListener implements ActionListener {
	private AbstractFrameConstructor frameOpener;
	private AbstractFrameConstructor frameCloser;

	public MainBangunDatarMenuViewSegitigaClickListener(AbstractFrameConstructor frameOpener, AbstractFrameConstructor frameCloser) {
		this.frameOpener = frameOpener;
		this.frameCloser = frameCloser;
	}

	@Override
	public void actionPerformed(ActionEvent arg0) {
		if(frameOpener != null) {
			frameOpener.show();
		}

		if(frameCloser != null) {
			frameCloser.hide();
		}
	}

}
```

#### Runner ####

Untuk menjalankan aplikasi yang baru kita buat, kita membutuhkan satu class lagi untuk menempatkan main class yang akan memanggil main bangun datar GUI yang telah dibuat.

```java
package javaintermediate.session3;

import javaintermediate.session3.gui.MainBangunDatarGui;

public class BangunDatarRunner {
	public static void main(String[] args) {
		MainBangunDatarGui gui = new MainBangunDatarGui();
		gui.show();
	}
}
```

