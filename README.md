CHAT APPLICATION USING JSOCKET CODE:
package main;
import com.formdev.flatlaf.FlatLightLaf;
import function.Client;
import function.Method;
import java.awt.Color;
import java.awt.Insets;
import java.io.File;
import java.net.ServerSocket;
import java.util.ArrayList;
import javax.swing.ImageIcon;
import javax.swing.JOptionPane;
import javax.swing.UIManager;
public class Main extends javax.swing.JFrame {
 public Main() {
 initComponents();
 setIconImage(new ImageIcon(getClass().getResource("/globalserver.png")).getImage());
 }
 @SuppressWarnings("unchecked")
 // <editor-fold defaultstate="collapsed" desc="Generated Code">//GENBEGIN:initComponents
 private void initComponents() {
 cmdStart = new javax.swing.JButton();
 cmdStop = new javax.swing.JButton();
 jScrollPane1 = new javax.swing.JScrollPane();
 txt = new javax.swing.JTextArea();
 lbStatus = new javax.swing.JLabel();
CHAPTER VIII
CODING
 setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
 setTitle("Global Server");
 cmdStart.setBackground(new java.awt.Color(102, 255, 102));
 cmdStart.setFont(new java.awt.Font("Victor Mono", 1, 13)); // NOI18N
 cmdStart.setText("Start Server");
 cmdStart.addActionListener(new java.awt.event.ActionListener() {
 public void actionPerformed(java.awt.event.ActionEvent evt) {
 cmdStartActionPerformed(evt);
 }
 });
 cmdStop.setBackground(new java.awt.Color(255, 102, 51));
 cmdStop.setFont(new java.awt.Font("Victor Mono", 1, 13)); // NOI18N
 cmdStop.setText("Stop Server");
 cmdStop.addActionListener(new java.awt.event.ActionListener() {
 public void actionPerformed(java.awt.event.ActionEvent evt) {
 cmdStopActionPerformed(evt);
 }
 });
 txt.setEditable(false);
 txt.setBackground(new java.awt.Color(0, 204, 204));
 txt.setColumns(20);
 txt.setFont(new java.awt.Font("Victor Mono", 1, 15)); // NOI18N
 txt.setRows(5);
 jScrollPane1.setViewportView(txt);
 lbStatus.setFont(new java.awt.Font("Victor Mono Oblique", 1, 13)); // NOI18N
 lbStatus.setForeground(new java.awt.Color(0, 51, 153));
 lbStatus.setText("//Server is Stop");
 javax.swing.GroupLayout layout = new 
javax.swing.GroupLayout(getContentPane());
 getContentPane().setLayout(layout);
 layout.setHorizontalGroup(
 layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
 .addGroup(layout.createSequentialGroup()
 .addContainerGap()
 
.addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADIN
G)
 .addComponent(jScrollPane1, 
javax.swing.GroupLayout.DEFAULT_SIZE, 631, Short.MAX_VALUE)
 .addGroup(layout.createSequentialGroup()
.addComponent(cmdStart)
 
.addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
 .addComponent(cmdStop)
 
.addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
 .addComponent(lbStatus, 
javax.swing.GroupLayout.PREFERRED_SIZE, 120, 
javax.swing.GroupLayout.PREFERRED_SIZE)
 .addGap(0, 0, Short.MAX_VALUE)))
 .addContainerGap())
 );
 layout.setVerticalGroup(
 layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
 .addGroup(layout.createSequentialGroup()
 .addContainerGap()
 
.addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELI
NE)
 .addComponent(cmdStart)
 .addComponent(cmdStop)
 .addComponent(lbStatus, javax.swing.GroupLayout.DEFAULT_SIZE, 
javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
 
.addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED, 7, 
Short.MAX_VALUE)
 .addComponent(jScrollPane1, javax.swing.GroupLayout.DEFAULT_SIZE, 
405, Short.MAX_VALUE)
 .addContainerGap())
 );
 pack();
 setLocationRelativeTo(null);
 }// </editor-fold>//GEN-END:initComponents
 private ServerSocket server;
 private Thread run;
 private void startServer() throws Exception {
 Method.setClients(new ArrayList<>());
 File f = new File("data");
 for (File fs : f.listFiles()) {
 fs.delete();
 }
 run = new Thread(new Runnable() {
 @Override
 public void run() {
 try {
 server = new ServerSocket(5000);
 lbStatus.setForeground(Color.GREEN);
 Method.setTxt(txt);
 txt.setText("Server now Starting ...\n");
 while (true) {
 new Client(server.accept());
 }
 } catch (Exception e) {
 JOptionPane.showMessageDialog(Main.this, e, "Error", 
JOptionPane.ERROR_MESSAGE);
 //e.printStackTrace();
 }
 }
 });
 run.start();
 }
 private void stopServer() throws Exception {
 int c = JOptionPane.showConfirmDialog(this, "Are you sure to stop server now", 
"Sotop Server", JOptionPane.YES_NO_OPTION, 
JOptionPane.QUESTION_MESSAGE);
 if (c == JOptionPane.YES_OPTION) {
 txt.setText("Server now Stoped ...");
 run.interrupt();
 server.close();
 }
 }
 private void cmdStartActionPerformed(java.awt.event.ActionEvent evt) {//GENFIRST:event_cmdStartActionPerformed
 try {
 int c = JOptionPane.showConfirmDialog(this, "File in data will be delete when 
server is start", "Start Server", JOptionPane.YES_NO_OPTION, 
JOptionPane.QUESTION_MESSAGE);
 if (c == JOptionPane.YES_OPTION) {
 startServer();
 }
 } catch (Exception e) {
 JOptionPane.showMessageDialog(this, e, "Error", 
JOptionPane.ERROR_MESSAGE);
 }
 }//GEN-LAST:event_cmdStartActionPerformed
rivate void cmdStopActionPerformed(java.awt.event.ActionEvent evt) {//GENFIRST:event_cmdStopActionPerformed
 try {
 stopServer();
 } catch (Exception e) {
 JOptionPane.showMessageDialog(this, e, "Error", 
JOptionPane.ERROR_MESSAGE);
 }
 }//GEN-LAST:event_cmdStopActionPerformed
 public static void main(String args[]) {
 FlatLightLaf.install();
 UIManager.put( "Button.arc", 999);
 UIManager.put( "Component.arc", 10 );
 UIManager.put( "Component.focusWidth", 1 );
 UIManager.put( "ProgressBar.arc", 999 );
 UIManager.put( "TextComponent.arc", 999 );
 UIManager.put( "ScrollBar.thumbArc", 999 );
 UIManager.put( "ScrollBar.thumbInsets", new Insets( 2, 2, 2, 2 ) );
 UIManager.put( "ScrollBar.thumb", new Color( 0xadd8e6) );
 UIManager.put( "TabbedPane.closeArc", 999 );
 UIManager.put( "Table.rowCellArc", 999 );
 UIManager.put( "TabbedPane.closeCrossFilledSize", 5.5f );
 UIManager.put( "TabbedPane.closeHoverForeground", Color.white );
 UIManager.put( "TabbedPane.closePressedForeground", Color.white );
 UIManager.put( "TabbedPane.closeHoverBackground", Color.red );
 UIManager.put( "TabbedPane.closePressedBackground", Color.red );
 java.awt.EventQueue.invokeLater(new Runnable() {
 @Override
 public void run() {
 new Main().setVisible(true);
 }
 });
 }
 // Variables declaration - do not modify//GEN-BEGIN:variables
 private javax.swing.JButton cmdStart;
 private javax.swing.JButton cmdStop;
 private javax.swing.JScrollPane jScrollPane1;
 private javax.swing.JLabel lbStatus;
 private javax.swing.JTextArea txt;
 // End of variables declaration//GEN-END:variables
}
