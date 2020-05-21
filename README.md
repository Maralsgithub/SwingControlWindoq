# SwingControlWindoq
This program creates a Java application that contains a Processing sketch and a Swing GUI. The Swing GUI contains a button that shows a color picker, and that color is sent to the Processing sketch to be displayed.

//At first, here’s the ProcessingSketch class:

public class ProcessingSketch extends PApplet{

	private float red = 64;
	private float green = 64;
	private float blue = 64;
	
	public void settings(){
		size(500, 500);
	}

	public void draw(){
		background(red, green, blue);
	}
	
	public void setColor(float red, float green, float blue) {
		this.red = red;
		this.green = green;
		this.blue = blue;
	}
	
	public void run(){
		String[] processingArgs = {"ProcessingSketch"};
		PApplet.runSketch(processingArgs, this);
	}

}

//This class contains variables that keep track of a color, a draw() function that displays that color, and a setColor() function that sets those variables. It also contains a run() function that calls the PApplet.runSketch() function to run this as a sketch. Notice that it uses the this keyword to pass itself in as a parameter.

//Here’s the SwingGui class:

import java.awt.Color;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JColorChooser;
import javax.swing.JFrame;

public class SwingGui {
	
	private JFrame frame;

	public SwingGui(ProcessingSketch sketch){
		frame = new JFrame("Controls");
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		
		JButton pickColor = new JButton("Color...");
		pickColor.addActionListener(new ActionListener(){
			
			@Override
			public void actionPerformed(ActionEvent e){
				Color color = JColorChooser.showDialog(pickColor, "Color Picker", Color.RED);
				sketch.setColor(color.getRed(), color.getGreen(), color.getBlue());
			}
		});
		
		frame.add(pickColor);
		frame.setSize(200, 100);
	}
	
	public void show(){
		frame.setVisible(true);
	}
}

//This class creates a Swing GUI that contains a button. When that button is pressed, the JColorChooser.showDialog() function is called, which allows the user to pick a color. That color is sent to the ProcessingSketch instance, which is passed in as a parameter.

//Finally, here’s the Main class:


public class Main {

	public static void main(String[] args){
		ProcessingSketch sketch = new ProcessingSketch();
		SwingGui swingGui = new SwingGui(sketch);
		
		sketch.run();
		swingGui.show();
	}
}

//This class just creates instances of the ProcessingSketch and SwingGui classes, passing the ProcessingSketch instance into the SwingGui constructor. Then it calls the run() and show() functions to display both screens:

