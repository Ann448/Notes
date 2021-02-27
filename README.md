package com.LTP.Notes;

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;
import java.io.FileOutputStream;
import java.io.FileWriter;
import java.io.IOException;
import java.io.Writer;
import java.nio.file.Files;
import java.nio.file.Paths;

import javax.swing.*;
//import javax.swing.SwingUtilities;
import javax.swing.event.AncestorListener;

public class Main {
	
	private final String NAME = "Новая тема";
	
	private JFileChooser f = new JFileChooser();
    
	//private static final String  = null;
       private JTabbedPane tabe = new JTabbedPane();
	public static void main(String[] arga) {
    	   
    	   SwingUtilities.invokeLater(new Runnable()  {
    	  
    		   public void run () {
    		   
    			   new Main();
    			 } 
     	   
        public Main() {
        	
        	JMenuBar menu = new JMenuBar();
        	
        	JMenu file = new JMenu("Биология");
        	
        	JMenuItem newFile = new JMenuItem("Дополнить Биология");
        	JMenuItem openFile = new JMenuItem("Открыть Биология");
        	JMenuItem saveFile = new JMenuItem("Сохранить изменения Биология");
        	
        	file.add(newFile);
        	file.add(openFile);
        	file.add(saveFile);
        	
        	menu.add(file);
        	
        	JFrame window = new JFrame("Notes");
        	window.setSize(800, 600);
        	
        	window.setJMenuBar(menu);
        	
        	window.add(tabe);
        	
        	
        	window.setResizable(false);
        	window.setLocationRelativeTo(null);
        	window.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        	window.setVisible(true);
	    
			newFile.addActionListener(new ActionListener() {
        		
        		public void actionPerformed(ActionEvent e) {
        			
        			JTextArea text = new JTextArea();
        			
        			Scroll scroll = new Scroll(text, false);
        			
        			tabe.addTab(NAME, scroll);

        		 } 
     	   });
               saveFile.addActionListener(new ActionListener() {
        		
        		public void actionPerformed(ActionEvent e) {
        			
        		if(tabe.countComponents() != 0) {        			
        			Scroll text = (Scroll)tabe.getSelectedComponent();
        			
        			String output = text.getText();
        			
        			f.showSaveDialog(null);
        			
        			File file = f.getSelectedFile();
        			
        			try{
        				FileOutputStream writer = new FileOutputStream (file);
        					writer.write(output.getBytes());
        			}catch(IOException eq){eq.printStackTrace();}
        	   } 
        		
        
           }
        		});		
               
			openFile.addActionListener(new ActionListener() {
        		
        		public void actionPerformed(ActionEvent e) {
        			try {
        		f.showDialog(null);
        		File file = f.getSelectedFile();
        
        		String input = new String(Files.readAllBytes(Paths.get(file.getAbsolutePath())));
                     
        		JTextArea text = new JTextArea (input);
        			
        		Scroll scroll = new Scroll(text, file.getName());
        		tabe.addTab(file.getName(), scroll);
        		
        	} catch (IOException el){el.printStackTrace();}
        				
        		 } 
        		
                
	           }
	        		});	
	     	 
