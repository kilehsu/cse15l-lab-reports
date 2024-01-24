# Lab Report 2

ChatServer Code:

~~~~
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String fullMsg = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return "Welcome to our ChatServer!";
        } 
        else if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                String message = parameters[1].substring(0, parameters[1].indexOf("&"));
                fullMsg += (String.format("%s: %s", parameters[2], message) + "\n");
                return fullMsg;
            }

        }
        return "404 Not Found!";
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
~~~~
