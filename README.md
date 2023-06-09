# chat_app_rmi
# Introduction :

Le projet d'application de chat est une application basée sur Java qui permet aux utilisateurs de communiquer en temps réel. L'application utilise la technologie Invocation de Méthode à Distance (RMI) pour la communication à distance entre les composants client et serveur. L'interface utilisateur graphique (GUI) de l'application est développée à l'aide de Swing, qui offre une interface conviviale pour l'envoi et la réception de messages.



## **RMI (Invocation de Méthode à Distance) :**

RMI est une technologie Java qui permet la communication entre des objets distribués dans un environnement en réseau. Elle permet aux objets Java s'exécutant sur différentes machines virtuelles Java (JVM) d'appeler des méthodes sur des objets distants comme s'ils étaient des objets locaux. RMI simplifie le développement de systèmes distribués en offrant un moyen transparent d'appeler des méthodes et d'échanger des données entre différentes machines.

RMI se compose des composants clés suivants :

1. **Interface distante :** Une interface distante est une interface qui déclare les méthodes qui peuvent être invoquées à distance par les clients. Elle étend l'interface `java.rmi.Remote`, et chaque déclaration de méthode doit lever `java.rmi.RemoteException`.

2. **Objet distant :** Un objet distant est une implémentation d'une interface distante. Il étend la classe `java.rmi.server.UnicastRemoteObject` pour le rendre disponible pour une invocation distante.

3. **Registre :** Le registre est un référentiel central où les objets distants sont enregistrés et peuvent être recherchés par les clients. Il est implémenté par la classe `java.rmi.registry.Registry` et fournit des méthodes pour lier et rechercher des objets distants.

4. **Stub et Skeleton :** Les stubs et les skeletons sont générés automatiquement par le compilateur RMI (`rmic`) en fonction de l'interface distante et de l'implémentation. Les stubs agissent comme des proxies côté client et transmettent les invocations de méthodes aux véritables objets distants. Les skeletons résident côté serveur et reçoivent les invocations de méthodes des clients et les délèguent aux objets distants correspondants.

5. **Serveur RMI :** Le serveur RMI héberge les objets distants et écoute les demandes entrantes des clients. Il est responsable de l'instanciation et de l'enregistrement des objets distants auprès du registre.

6. **Client RMI :** Le client RMI lance des invocations de méthodes à distance sur des objets distants. Il recherche les objets distants dans le registre et obtient des stubs pour invoquer des méthodes à distance.

RMI offre un mécanisme transparent de communication à distance, permettant aux développeurs de travailler avec des objets distribués comme s'ils étaient des objets locaux. Elle simplifie le développement d'applications distribuées en abstrayant les complexités de la communication réseau.

## **Swing :**

Swing est une bibliothèque Java pour l'interface graphique (Graphical User Interface ou GUI), fournie par les Java Foundation Classes (JFC). Elle permet aux développeurs de créer des interfaces graphiques riches, interactives et indépendantes de la plateforme pour les applications Java. Swing offre un ensemble complet de composants, de conteneurs, de gestionnaires de disposition (layout managers) et de mécanismes de gestion des événements pour créer des interfaces utilisateur conviviales.

Les fonctionnalités clés et les composants de Swing comprennent :

1. **JFrame :** Il s'agit d'un conteneur de premier niveau qui représente la fenêtre principale d'une application Swing.

2. **JPanel :** Il

 s'agit d'un conteneur léger qui peut être utilisé pour organiser et regrouper des composants.

3. **JLabel :** Il s'agit d'un composant pour afficher du texte ou une image.

4. **JButton :** Il s'agit d'un composant de bouton qui permet aux utilisateurs d'effectuer des actions lorsqu'il est cliqué.

5. **JTextField :** Il s'agit d'un composant de champ de texte permettant aux utilisateurs de saisir du texte.

6. **JTextArea :** Il s'agit d'un composant de zone de texte multiligne pour afficher ou saisir du texte sur plusieurs lignes.

7. **JScrollPane :** Il s'agit d'un composant qui ajoute des barres de défilement à d'autres composants lorsque le contenu dépasse la zone visible.

8. **Gestionnaires de disposition (layout managers) :** Swing offre une variété de gestionnaires de disposition pour organiser les composants dans une fenêtre, tels que `BorderLayout`, `FlowLayout`, `GridLayout`, etc.

Swing facilite la création d'interfaces utilisateur attrayantes et interactives pour les applications Java. Grâce à sa flexibilité et à sa portabilité, il est largement utilisé pour le développement d'applications de bureau et d'applications basées sur l'interface utilisateur.

# Project:

Le projet est composé de plusieurs classes Java qui gèrent différentes fonctionnalités de l'application de chat. Voici un aperçu des principales classes et de leurs fonctionnalités :

**ChatWindow.java :** Cette classe représente la fenêtre principale de l'interface graphique de l'application de chat. Elle étend la classe JFrame de Swing et fournit des zones de texte, des champs de texte et des boutons pour l'interaction avec l'utilisateur. Elle inclut également des méthodes pour gérer l'envoi et la réception de messages, afficher les clients connectés, se déconnecter du serveur et envoyer des fichiers.

**ChatClient.java :** Cette interface définit les méthodes distantes qui peuvent être appelées par le serveur du côté client. Elle inclut des méthodes pour la réception de messages, l'envoi de messages, la déconnexion du serveur, l'obtention du nom du client et l'envoi de fichiers.

**ChatClientImpl.java :** Cette classe implémente l'interface ChatClient. Elle étend la classe UnicastRemoteObject, ce qui permet à l'objet d'être utilisé comme objet distant. Elle représente l'implémentation côté client et fournit des méthodes pour la réception de messages, l'envoi de messages, la déconnexion du serveur, l'obtention du nom du client et l'envoi de fichiers. Elle crée également une instance de la classe ChatWindow pour l'interface graphique du client.

**ChatServer.java :** Cette interface définit les méthodes distantes qui peuvent être appelées par les clients du côté serveur. Elle inclut des méthodes pour l'enregistrement et la désinscription des clients, la diffusion de messages à tous les clients et la réception de fichiers des clients.

**ChatServerImpl.java :** Cette classe implémente l'interface ChatServer. Elle étend la classe UnicastRemoteObject et représente l'implémentation côté serveur. Elle fournit des méthodes pour l'enregistrement et la désinscription des clients, la diffusion de messages à tous les clients et la réception de fichiers des clients. Elle maintient une liste des clients connectés et les informe des nouveaux clients rejoignant ou quittant le chat.


# ChatWindow :

Partie 1:
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.rmi.RemoteException;
import javax.swing.JOptionPane;
```
Dans cette partie, les importations nécessaires sont ajoutées. Elles incluent des classes Swing pour l'interface utilisateur, des classes AWT pour la disposition des composants, des classes d'événements ActionListener pour la gestion des actions et des classes liées à la communication à distance (RemoteException) et aux boîtes de dialogue (JOptionPane).

Partie 2:
```java
public class ChatWindow extends JFrame {
    private JTextArea clientArea; 
    private JTextArea chatArea;
    private JTextField nameField; 
    private JTextField messageField;
    private JButton sendButton;
    private JButton disconnectButton; 
    private JButton sendFileButton; 
    private ChatClient client;
```
Dans cette partie, une classe `ChatWindow` est définie, qui hérite de la classe `JFrame`. Elle contient des variables pour les différents composants de l'interface graphique, tels que les zones de texte (`clientArea` et `chatArea`), les champs de texte (`nameField` et `messageField`), les boutons (`sendButton`, `disconnectButton` et `sendFileButton`), ainsi qu'une variable `client` de type `ChatClient` utilisée pour la communication.

Partie 3:
```java
public ChatWindow(ChatClient client) {
    this.client = client;

    setTitle("Chat App");
    setSize(400, 300);
    setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
```
Dans cette partie, le constructeur de la classe `ChatWindow` est défini. Il prend un objet `ChatClient` en paramètre et l'assigne à la variable `client`. Ensuite, il configure les paramètres de base de la fenêtre, tels que le titre, la taille et l'opération de fermeture.

Partie 4:
```java
clientArea = new JTextArea(); // Added: JTextArea to display connected clients
clientArea.setEditable(false);
JScrollPane clientScrollPane = new JScrollPane(clientArea);
add(clientScrollPane, BorderLayout.WEST);

chatArea = new JTextArea();
chatArea.setEditable(false);
JScrollPane chatScrollPane = new JScrollPane(chatArea);
add(chatScrollPane, BorderLayout.CENTER);

JPanel topPanel = new JPanel(new BorderLayout());
JLabel nameLabel = new JLabel("Name:");
nameField = new JTextField();
topPanel.add(nameLabel, BorderLayout.WEST);
topPanel.add(nameField, BorderLayout.CENTER);
add(topPanel, BorderLayout.NORTH);

JPanel bottomPanel = new JPanel(new BorderLayout());

messageField = new JTextField();
bottomPanel.add(messageField, BorderLayout.CENTER);

sendButton = new JButton("Send");
sendButton.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        sendMessage();
    }
});
bottomPanel.add(sendButton, BorderLayout.EAST);

disconnectButton = new JButton("Disconnect"); // Added: JButton to disconnect
disconnectButton.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        disconnect();
    }
});
bottomPanel.add(disconnectButton, BorderLayout.WEST);

sendFileButton = new JButton("Send File"); // Added: JButton to send files
sendFileButton.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        sendFile();
    }
});
bottomPanel.add(sendFileButton, BorderLayout.SOUTH);

add(bottomPanel, BorderLayout.SOUTH);
```
Dans cette partie, les composants de l'interface graphique sont créés et configurés. Voici ce qui se passe :
- Une zone de texte `clientArea` est créée pour

 afficher les clients connectés. Elle est rendue non éditable et est placée dans un `JScrollPane` pour permettre le défilement si nécessaire.
- Une zone de texte `chatArea` est créée pour afficher les messages de chat. Elle est rendue non éditable et est placée dans un autre `JScrollPane`.
- Un panneau supérieur (`topPanel`) est créé avec une disposition `BorderLayout`. Il contient une étiquette (`nameLabel`) et un champ de texte (`nameField`) pour saisir le nom de l'utilisateur.
- Un panneau inférieur (`bottomPanel`) est créé avec une disposition `BorderLayout`. Il contient un champ de texte (`messageField`) pour saisir les messages à envoyer.
- Un bouton `sendButton` est créé avec le texte "Send" et un écouteur d'événements qui appelle la méthode `sendMessage()` lorsqu'il est cliqué.
- Un bouton `disconnectButton` est créé avec le texte "Disconnect" et un écouteur d'événements qui appelle la méthode `disconnect()` lorsqu'il est cliqué.
- Un bouton `sendFileButton` est créé avec le texte "Send File" et un écouteur d'événements qui appelle la méthode `sendFile()` lorsqu'il est cliqué.
- Tous les composants sont ajoutés à la fenêtre en utilisant la disposition `BorderLayout`.

Cette partie configure l'apparence et l'interaction des composants de l'interface graphique de la fenêtre de chat.

Partie 5:
```java
public void appendMessage(String message) {
    chatArea.append(message + "\n");
}

public void appendClient(String clientName) { // Added: Display a connected client
    clientArea.append(clientName + "\n");
}

public String getMessage() {
    return messageField.getText();
}

public String getName() { 
    return nameField.getText();
}

public void clearMessageField() {
    messageField.setText("");
}
```
Cette partie contient des méthodes pour gérer les actions de la fenêtre de chat. Voici ce que font ces méthodes :
- La méthode `appendMessage(String message)` ajoute un message à la zone de texte `chatArea`. Le message est suivi d'un saut de ligne pour s'afficher sur une nouvelle ligne.
- La méthode `appendClient(String clientName)` ajoute un nom de client à la zone de texte `clientArea`, affichant ainsi les clients connectés. Chaque nom de client est affiché sur une nouvelle ligne.
- La méthode `getMessage()` retourne le contenu du champ de texte `messageField`, qui contient le message saisi par l'utilisateur.
- La méthode `getName()` retourne le contenu du champ de texte `nameField`, qui contient le nom de l'utilisateur.
- La méthode `clearMessageField()` efface le contenu du champ de texte `messageField`.

Ces méthodes permettent de manipuler et de récupérer les données saisies par l'utilisateur dans les champs de texte et de mettre à jour les zones de texte avec les messages et les clients connectés.

Partie 6:
```java
private void sendMessage() {
    String message = getMessage();
    if (!message.isEmpty()) {
        try {
            String name = client.getName();
            client.sendMessage(name, message);
            appendMessage(name + ": " + message);
            clearMessageField();
        } catch (RemoteException e) {
            e.printStackTrace();
        }
    }
}
```
Cette partie contient la méthode `sendMessage()`, qui est appelée lorsque l'utilisateur clique sur le bouton "Send". Voici ce qu'elle fait :
- Elle récupère le message saisi par l'utilisateur à l'aide de la méthode `getMessage()`.
- Si le message n'est pas vide, elle récupère le nom de l'utilisateur à partir de l'objet `client` en utilisant la méthode `getName()`.
- Elle appelle la méthode `sendMessage(name, message)` de l'objet `client` pour envoyer le message au serveur.
- Elle ajoute le message à la zone de texte `chatArea` en l'affichant avec le nom de l'utilisateur.
- Elle efface le champ de texte `messageField` en appelant la méthode `clearMessageField()`.
- En cas d'erreur lors de l'appel de la méthode `sendMessage()` (par exemple, une exception `RemoteException`), elle affiche la trace de la pile d'erreurs.

Cette méthode permet d'envoyer un message au serveur en utilisant l'objet `client` pour la communication.

Partie 7:
```java
private String getClientName() {
    return JOptionPane.showInputDialog("Enter your name:"); 
}

private void disconnect() { 
    try {
        client.disconnect();
        System.exit(0);
    } catch (RemoteException e) {
        e.printStackTrace();
    }
}
```
Cette partie contient deux méthodes :
- La méthode `getClientName()` ouvre une boîte de dialogue où l'utilisateur peut saisir son nom. Elle utilise la classe `JOptionPane` pour afficher une boîte de dialogue et récupère le nom saisi.
- La méthode `

disconnect()` est appelée lorsque l'utilisateur clique sur le bouton "Disconnect". Elle appelle la méthode `disconnect()` de l'objet `client` pour se déconnecter du serveur, puis elle quitte l'application en appelant `System.exit(0)`. En cas d'erreur lors de la déconnexion, elle affiche la trace de la pile d'erreurs.

Ces deux méthodes permettent à l'utilisateur de se connecter avec un nom d'utilisateur et de se déconnecter du serveur.

Partie 8:
```java
private void sendFile() { // Added: Send a file
    // Implement the file sending functionality here
    JFileChooser fileChooser = new JFileChooser();
    int result = fileChooser.showOpenDialog(this);
    if (result == JFileChooser.APPROVE_OPTION) {
        File fileToSend = fileChooser.getSelectedFile();

        // Read the selected file as byte data
        byte[] fileData = Files.readAllBytes(fileToSend.toPath());

        // Get the file name
        String fileName = fileToSend.getName();

        // Send the file to the server
        client.sendFile(fileName, fileData);

        // Display a message in the chat area that the file is being sent
        appendMessage("Me: Sending file - " + fileName);
        clearMessageField();
    }
}
```
Cette partie contient la méthode `sendFile()`, qui est appelée lorsque l'utilisateur clique sur le bouton "Send File". Voici ce qu'elle fait :
- Elle ouvre une boîte de dialogue de sélection de fichier en utilisant la classe `JFileChooser` pour permettre à l'utilisateur de choisir un fichier à envoyer.
- Si l'utilisateur sélectionne un fichier et clique sur "OK", elle récupère le fichier sélectionné en utilisant la méthode `getSelectedFile()` de l'objet `fileChooser`.
- Elle lit le contenu du fichier sélectionné sous forme de tableau d'octets en utilisant la classe `Files` et la méthode `readAllBytes()`.
- Elle récupère le nom du fichier en utilisant la méthode `getName()` de l'objet `fileToSend`.
- Elle appelle la méthode `sendFile(fileName, fileData)` de l'objet `client` pour envoyer le fichier au serveur.
- Elle ajoute un message dans la zone de texte `chatArea` pour indiquer que le fichier est en cours d'envoi.
- Elle efface le champ de texte `messageField` en appelant la méthode `clearMessageField()`.

Cette méthode permet à l'utilisateur de sélectionner et d'envoyer un fichier au serveur en utilisant l'objet `client`. Le contenu du fichier est lu et envoyé en tant que tableau d'octets.

# ChatClient :

**Partie 1 :**

```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface ChatClient extends Remote {
```
Cette partie définit l'interface `ChatClient` qui étend l'interface `Remote`. L'interface `Remote` est utilisée dans le contexte de RMI (Remote Method Invocation) pour indiquer que cette interface peut être utilisée pour appeler des méthodes à distance.

**Partie 2 :**

```java
    void receiveMessage(String message) throws RemoteException;
    void sendMessage(String name, String message) throws RemoteException;
    void disconnect() throws RemoteException;
    String getName() throws RemoteException;
    void sendFile(String fileName, byte[] fileData) throws RemoteException;
}
```
Cette partie déclare les méthodes nécessaires pour un client de chat. Voici ce que font ces méthodes :

- La méthode `receiveMessage(String message)` est appelée par le serveur pour envoyer un message au client. Elle prend en paramètre le message reçu. Elle lève une exception `RemoteException` pour gérer les erreurs liées à la communication à distance.

- La méthode `sendMessage(String name, String message)` est utilisée par le client pour envoyer un message au serveur. Elle prend en paramètres le nom de l'utilisateur et le message à envoyer. Elle lève une exception `RemoteException` pour gérer les erreurs liées à la communication à distance.

- La méthode `disconnect()` est utilisée par le client pour se déconnecter du serveur. Elle lève une exception `RemoteException` pour gérer les erreurs liées à la communication à distance.

- La méthode `getName()` est utilisée par le client pour obtenir le nom de l'utilisateur. Elle renvoie une chaîne de caractères représentant le nom de l'utilisateur. Elle lève une exception `RemoteException` pour gérer les erreurs liées à la communication à distance.

- La méthode `sendFile(String fileName, byte[] fileData)` est utilisée par le client pour envoyer un fichier au serveur. Elle prend en paramètres le nom du fichier et les données du fichier sous forme de tableau d'octets. Elle lève une exception `RemoteException` pour gérer les erreurs liées à la communication à distance.

Ces méthodes définissent les fonctionnalités nécessaires pour la communication entre le client et le serveur de chat. Elles sont destinées à être implémentées par une classe cliente qui utilise cette interface.


# ChatClientImpl :


Partie 1 :
```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;
import javax.swing.JOptionPane;

public class ChatClientImpl extends UnicastRemoteObject implements ChatClient {
    private ChatWindow chatWindow;
    private ChatServer server;
    private String clientName;

    public ChatClientImpl(ChatServer server, String clientName) throws RemoteException {
        this.clientName = clientName;
        this.server = server;
        server.registerClient(this);
        chatWindow = new ChatWindow(this);
        chatWindow.setVisible(true);
    }
```
Cette partie de code définit la classe `ChatClientImpl` qui implémente l'interface `ChatClient` et étend la classe `UnicastRemoteObject`, qui est une classe fournie par RMI pour faciliter la création d'objets distants.

La classe `ChatClientImpl` possède les membres suivants :
- `chatWindow` : une instance de la classe `ChatWindow` utilisée pour afficher l'interface graphique du client de chat.
- `server` : une référence au serveur de chat auquel le client est connecté.
- `clientName` : le nom du client.

Le constructeur `ChatClientImpl` est appelé lorsqu'un client de chat est créé. Il prend en paramètres le serveur de chat et le nom du client. Dans ce constructeur, le client s'enregistre auprès du serveur en appelant la méthode `registerClient(this)` du serveur, puis crée et affiche une fenêtre de chat (`ChatWindow`).

Partie 2 :
```java
    @Override
    public void receiveMessage(String message) throws RemoteException {
        if (chatWindow != null) {
            chatWindow.appendMessage(message);
        }
    }
```
Cette partie représente l'implémentation de la méthode `receiveMessage` définie dans l'interface `ChatClient`. Cette méthode est appelée par le serveur pour envoyer un message au client. Elle vérifie d'abord si la fenêtre de chat (`chatWindow`) existe, puis appelle la méthode `appendMessage` de la fenêtre de chat pour afficher le message reçu.

Partie 3 :
```java
    @Override
    public void sendMessage(String name, String message) throws RemoteException {
        server.broadcastMessage(name, message);
    }
```
Cette partie représente l'implémentation de la méthode `sendMessage` définie dans l'interface `ChatClient`. Cette méthode est utilisée par le client pour envoyer un message au serveur. Elle prend en paramètres le nom de l'utilisateur et le message à envoyer. Elle appelle ensuite la méthode `broadcastMessage` du serveur pour diffuser le message à tous les clients connectés.

Partie 4 :
```java
    @Override
    public void disconnect() throws RemoteException {
        server.unregisterClient(this);
    }
```
Cette partie représente l'implémentation de la méthode `disconnect` définie dans l'interface `ChatClient`. Cette méthode est utilisée par le client pour se déconnecter du serveur. Elle appelle la méthode `unregisterClient` du serveur pour retirer le client de la liste des clients connectés.

Partie 5 :
```java
    @Override
    public String getName() throws RemoteException {
        return clientName;
    }
```
Cette partie représente l'implémentation de la méthode `getName` définie dans l'interface `ChatClient`. Cette méthode est

 utilisée par le client pour obtenir le nom de l'utilisateur. Elle renvoie simplement le nom du client.

Partie 6 :
```java
    @Override
    public void sendFile(String fileName, byte[] fileData) throws RemoteException {
        try {
            server.receiveFile(clientName, fileName, fileData);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
Cette partie représente l'implémentation de la méthode `sendFile` définie dans l'interface `ChatClient`. Cette méthode est utilisée par le client pour envoyer un fichier au serveur. Elle prend en paramètres le nom du fichier et les données du fichier sous forme de tableau d'octets. Elle appelle ensuite la méthode `receiveFile` du serveur en lui passant le nom du client, le nom du fichier et les données du fichier.

Partie 7 :
```java
    public static void main(String[] args) {
        try {
            String serverIP = "localhost";
            ChatServer server = (ChatServer) java.rmi.Naming.lookup("rmi://" + serverIP + "/ChatServer");
            String name = JOptionPane.showInputDialog("Enter your name:");  // Prompt the user to enter their name
            ChatClientImpl client = new ChatClientImpl(server, name);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
Cette partie représente la méthode `main` de la classe `ChatClientImpl`. Cette méthode est exécutée lorsque le programme est lancé. Elle effectue les opérations suivantes :
- Elle récupère une référence au serveur de chat en utilisant `java.rmi.Naming.lookup` pour rechercher le serveur à l'adresse `rmi://localhost/ChatServer`.
- Elle demande à l'utilisateur de saisir son nom en utilisant la classe `JOptionPane` pour afficher une boîte de dialogue.
- Elle crée une instance de `ChatClientImpl` en passant la référence du serveur et le nom de l'utilisateur.

# ChatServer :


Partie 1 :
```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface ChatServer extends Remote {
    void registerClient(ChatClient client) throws RemoteException;
    void unregisterClient(ChatClient client) throws RemoteException;
```
Cette partie de code définit l'interface `ChatServer` qui étend l'interface `Remote`, ce qui indique qu'elle peut être utilisée pour créer des objets distants.

L'interface `ChatServer` expose les méthodes suivantes :
- `registerClient` : Cette méthode est utilisée pour enregistrer un client auprès du serveur. Elle prend en paramètre une référence à un objet de type `ChatClient` qui représente le client à enregistrer.
- `unregisterClient` : Cette méthode est utilisée pour désenregistrer un client du serveur. Elle prend en paramètre une référence à un objet de type `ChatClient` qui représente le client à désenregistrer.

Partie 2 :
```java
    void broadcastMessage(String senderName, String message) throws RemoteException;
    void receiveFile(String clientName, String fileName, byte[] fileData) throws RemoteException, IOException;
}
```
Cette partie de code définit les autres méthodes de l'interface `ChatServer` :
- `broadcastMessage` : Cette méthode est utilisée pour diffuser un message à tous les clients connectés. Elle prend en paramètres le nom de l'expéditeur du message (`senderName`) et le contenu du message lui-même (`message`).
- `receiveFile` : Cette méthode est utilisée pour recevoir un fichier envoyé par un client. Elle prend en paramètres le nom du client qui envoie le fichier (`clientName`), le nom du fichier (`fileName`) et les données du fichier sous forme de tableau d'octets (`fileData`). Cette méthode peut également générer une exception de type `IOException` si une erreur se produit lors de la réception du fichier.

Ces méthodes définissent les fonctionnalités principales du serveur de chat, telles que l'enregistrement et le désenregistrement des clients, la diffusion de messages à tous les clients et la réception de fichiers envoyés par les clients.

# ChatServerImpl :


Partie 1 :
```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;
import java.util.ArrayList;
import java.util.List;
import javax.swing.JOptionPane;
import java.rmi.Naming;

public class ChatServerImpl extends UnicastRemoteObject implements ChatServer {
```
Cette partie de code définit la classe `ChatServerImpl` qui étend la classe `UnicastRemoteObject` et implémente l'interface `ChatServer`. La classe `UnicastRemoteObject` fournit une implémentation par défaut des fonctionnalités nécessaires pour prendre en charge l'appel à distance des méthodes.

La classe `ChatServerImpl` contient les membres suivants :
- `clients` : Une liste qui stocke les références des clients connectés au serveur.

Partie 2 :
```java
    public ChatServerImpl() throws RemoteException {
        clients = new ArrayList<>();
    }
```
Ce constructeur initialise la liste des clients lorsqu'une instance de `ChatServerImpl` est créée.

Partie 3 :
```java
    @Override
    public void registerClient(ChatClient client) throws RemoteException {
        clients.add(client);
        notifyClients(client.getName() + " has joined the chat."); // Notify clients about the new client
    }

    @Override
    public void unregisterClient(ChatClient client) throws RemoteException {
        clients.remove(client);
        notifyClients(client.getName() + " has left the chat."); // Notify clients about the departing client
    }
```
Ces méthodes permettent d'enregistrer et de désenregistrer un client auprès du serveur. Lorsqu'un client est enregistré, sa référence est ajoutée à la liste des clients et les autres clients sont notifiés de son arrivée. De même, lorsqu'un client est désenregistré, sa référence est supprimée de la liste des clients et les autres clients sont notifiés de son départ.

Partie 4 :
```java
    @Override
    public void broadcastMessage(String senderName, String message) throws RemoteException {
        for (ChatClient client : clients) {
            if (!client.getName().equals(senderName)) {
                client.receiveMessage(senderName + ": " + message);
            }
        }
    }
```
Cette méthode permet de diffuser un message à tous les clients connectés, à l'exception de l'expéditeur du message. Elle parcourt la liste des clients et appelle la méthode `receiveMessage` de chaque client pour lui transmettre le message.

Partie 5 :
```java
    private void notifyClients(String message) throws RemoteException {
        for (ChatClient client : clients) {
            client.receiveMessage(message);
        }
    }
```
Cette méthode permet de notifier tous les clients connectés en leur envoyant un message donné. Elle parcourt la liste des clients et appelle la méthode `receiveMessage` de chaque client pour lui transmettre le message.

Partie 6 :
```java
    @Override
    public void receiveFile(String clientName, String fileName, byte[] fileData) throws RemoteException, IOException {
      
        String filePath = "path/to/save/files/" + fileName;
        FileOutputStream fileOutputStream = new FileOutputStream(filePath);
        fileOutputStream.write(fileData);
        fileOutputStream.close();
        

        String message =

 clientName + " sent a file: " + fileName;
        broadcastMessage(message);
    }
```
Cette méthode permet de recevoir un fichier envoyé par un client. Elle prend en paramètres le nom du client qui envoie le fichier (`clientName`), le nom du fichier (`fileName`) et les données du fichier sous forme de tableau d'octets (`fileData`).

Dans cette méthode, vous devez implémenter la logique nécessaire pour recevoir le fichier côté serveur. Dans l'exemple donné, le fichier est enregistré dans un répertoire spécifique en utilisant un `FileOutputStream`.

Une fois le fichier reçu et enregistré, un message est diffusé à tous les clients pour les informer de la réception du fichier.

Partie 7 :
```java
    public static void main(String[] args) {
        try {
            ChatServer server = new ChatServerImpl();
            Naming.rebind("ChatServer", server);
            System.out.println("ChatServer bound in the registry.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```
La méthode `main` est utilisée pour démarrer le serveur de chat. Elle crée une instance de `ChatServerImpl`, la relie au registre RMI en utilisant la méthode `rebind`, et affiche un message de confirmation si l'opération réussit.

# Test :

Compilez tous les fichiers source du projet à l'aide du compilateur Java

```java
javac *.java
```

On démarre le registre RMI en exécutant la commande suivante 

```java
start rmiregistry

```
![4](https://github.com/zaka1200/chat_app_rmi/assets/121964432/df038e20-f2ab-409a-91fd-6a744e98d935)

On démarre le serveur de chat en exécutant la classe ChatServerImpl

```java
java ChatServerImpl.java
```
Puis on exécute le client en exécutant la classe ChatClientImpl

```java
java ChatClientImpl.java
```
on vas exécuter plusieurs instances du client sur la même machine

on commence par s'authentifier :

![1](https://github.com/zaka1200/chat_app_rmi/assets/121964432/a1940e51-a50d-4910-abe5-8a9b0f31d8d1)

maintenant on peut assurer une communication entre les client

![2](https://github.com/zaka1200/chat_app_rmi/assets/121964432/16f6e913-de07-4fba-84dd-f3d5f6c65179)

![3](https://github.com/zaka1200/chat_app_rmi/assets/121964432/8387ac01-8842-4e68-91c7-ceca908189aa)


# Conclusion :

En conclusion, le code présenté implémente un système de chat distribué en utilisant la technologie RMI (Remote Method Invocation). Il se compose de plusieurs classes, dont ChatWindow, ChatClient, ChatServer, ChatClientImpl et ChatServerImpl, qui travaillent ensemble pour permettre la communication entre les clients connectés au serveur de chat.

La classe ChatWindow représente la fenêtre de chat côté client, offrant une interface utilisateur pour envoyer des messages, se déconnecter et envoyer des fichiers. Elle interagit avec la classe ChatClient qui gère les actions du client et communique avec le serveur.

Le serveur de chat est implémenté par la classe ChatServerImpl, qui enregistre les clients connectés, gère l'envoi et la réception de messages, ainsi que l'envoi et la réception de fichiers. La classe ChatClientImpl représente l'implémentation côté client du chat, qui se connecte au serveur et utilise la fenêtre de chat pour interagir avec l'utilisateur.

Dans l'ensemble, ce système de chat distribué permet aux utilisateurs de communiquer en temps réel en échangeant des messages et des fichiers. Il illustre l'utilisation de RMI pour la communication entre les différentes parties du système.
