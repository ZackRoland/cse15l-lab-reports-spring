## **PART 1:**

## Code:
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
        String chatHistory = "";

        public String handleRequest(URI url){
                if (url.getPath().equals("/")){
                        return chatHistory;
                }

                if (url.getPath().equals("/add-message")){
                        String[] params = url.getQuery().split("&");
                        String[] messageParam = params[0].split("=");
                        String[] userParam = params[1].split("=");
                        if (messageParam[0].equals("s") && userParam[0].equals("user")){
                                String message = messageParam[1];
                                String user = userParam[1];
                                this.chatHistory += user + ": " + message+"\n";
                                return this.chatHistory;
                        }
                }
                return "404 Not Found";
        }
}
class ChatServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0){
                System.out.println("Missing port number! Try any number between 1024 to 49151");
                return;
        }
        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
  }
}
```
## Screenshot 1 Path(/add-message?s=Dereshishishi&user=JaguarD.Saul):
![Path 1](https://i.postimg.cc/tTHr5Szr/CSE-15-L-LAB-2-SS-1.png)
1. The method the code called is the handleRequest method. This method takes in a url as
   input and displays the user and their subsequent message.
2. The relevant arguments to this method is the url which is what this method works with.
   The main field this class utilizes is the chatHistory field which is a string that holds
   all the messages within it. We also have fields param, messageParam, userParam, message, and user.
   Which hold the query and the various parts of it.
3. The params field gets updated with the query in 2 parts, "s=Dereshishishi" and "user=JaguarD.Saul".
   The messageParam field then gets updated with the first param into 2 parts "s" and "Dereshishishi"
   while the userParam field gets updated with the second param into 2 parts "user" and "JaguarD.Saul".
   message gets updated with just the second part of the messageParam field "Dereshishishi" and user gets
   updated with the second part of the userParam field "JaguarD.Saul". Finally, the chatHistory field gets
   updated with both the user and message to return "JaguarD.Saul: Dereshishishi".
## Screenshot 2 Path(/add-message?s=Meatttttt&user=MonkeyD.Luffy):
![Path 2](https://i.postimg.cc/hG48PkpR/CSE-15-L-LAB-2-SS2.png)
1. The method the code called isis the handleRequest method. This method takes in a url as
   input and displays the user and their subsequent message.
2. The relevant arguments to this method is the url which is what this method works with.
   The main field this class utilizes is the chatHistory field which is a string that holds
   all the messages within it. We also have fields param, messageParam, userParam, message, and user.
   Which hold the query and the various parts of it.
3. The params field gets updated with the query in 2 parts, "s=Meatttttt" and "user=MonkeyD.Luffy".
   The messageParam field then gets updated with the first param into 2 parts "s" and "Meatttttt"
   while the userParam field gets updated with the second param into 2 parts "user" and "MonkeyD.Luffy".
   message gets updated with just the second part of the messageParam field "Meatttttt" and user gets
   updated with the second part of the userParam field "MonkeyD.Luffy". Finally, the chatHistory field gets
   updated with both the user and message to return the message previously stored in chatHistory and also
   the new user and their message.

## **PART 2:**

# PUBLIC KEY
![Public Key](https://i.postimg.cc/4dxmcZ9s/CSE-15-L-LAB-2-SS3.png)
# PRIVATE KEY
![Private Key](https://i.postimg.cc/qMvHdqdk/CSE-15-L-LAB-2-SS-4.png)
# Terminal Interaction
![Terminal Interaction](https://i.postimg.cc/P5vct8Vk/CSE-15-L-LAB-2-SS-5.png)

## **PART 3:**
> What I learned from lab in week's 2 and 3 that I didn't know before was how to generate my own server
> that takes in input via the path and query's it is given. I feel like this could have applications for
> much larger uses for web development purposes if I choose to ever delve into that type of stuff.

