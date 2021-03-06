# SystemTray
# How to Use the System Tray.


The system tray is a specialized area of the desktop where users can access currently running programs. This area may be referred to differently on various operating systems. On Microsoft Windows, the system tray is referred to as the Taskbar Status Area, while on the GNU Network Object Model Environment (GNOME) Desktop it is referred to as the Notification Area. On K Desktop Environment (KDE) this area is referred to as the System Tray. However, on each system the tray area is shared by all applications running on the desktop.
More information can be found on [https://docs.oracle.com/](https://docs.oracle.com/javase/tutorial/uiswing/misc/systemtray.html).


## SystemTrayManager.java


package com.wikidreams.systemtray;

import java.awt.AWTException;
import java.awt.MenuItem;
import java.awt.PopupMenu;
import java.awt.SystemTray;
import java.awt.TrayIcon;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseAdapter;
import java.awt.event.MouseEvent;
import javax.swing.ImageIcon;

public class SystemTrayManager {

	private static TrayIcon trayIcon;
	private static PopupMenu menu;
	private static ImageIcon icon;
	private static String iconTitle = "Demo";
	private static String baloonTitle = "Application";
	private static String ballonMessage = "Running on system tray.";

	public static void CreateSystemTrayManager() {
		if (! SystemTray.isSupported()) {
			System.out.println("The system does not supports system tray.");
			System.exit(0);
		}
		CreateSystemTrayMenu();
	}


	private static void CreateSystemTrayMenu() {
		menu = new PopupMenu();

		MenuItem exitItem = new MenuItem("Exit");
		exitItem.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				System.exit(0);
			}
		});

		menu.add(exitItem);
		CreateSystemTrayIcon();
	}


	private static void CreateSystemTrayIcon() {
		icon = new ImageIcon("images/icone.gif");
		trayIcon = new TrayIcon(icon.getImage(), iconTitle, menu);
		trayIcon.addMouseListener(new MouseAdapter() {
			@Override
			public void mouseClicked(MouseEvent e) {
				if (e.getClickCount() == 2) {
					SystemTray.getSystemTray().remove(trayIcon);
				} 
			}            
		});
		AddToSystemTray();
	}


	private static void AddToSystemTray() {
		try {
			SystemTray.getSystemTray().add(trayIcon);
			trayIcon.displayMessage(baloonTitle, ballonMessage, TrayIcon.MessageType.INFO);
		} catch (AWTException ex) {
			System.out.println(ex.getMessage());
		}
	}

}


## App.java


package com.wikidreams.systemtray;

public class 	 App {

	public static void main(String[] args) {
		SystemTrayManager.CreateSystemTrayManager();		
	}

}


Produced by [Wiki Dreams.github.io](https://WikiDreams.github.io/).