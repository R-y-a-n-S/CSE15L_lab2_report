# Lab Report 2
## Part 1
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String out = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(out);
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    out += parameters[1] + "\n";
                    // System.out.println(out);
                    return String.format(out);
                }
            }
            return "404 Not Found!";
        }
    }
}

class myServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```
## Part 2 
The following refers to the reversed method in Array.
- Failure inducing input: 

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test 
  public void testReversed() {
      int[] input2 = {7,5,3};
      assertArrayEquals(new int[]{3,5,7}, ArrayExamples.reversed(input2));
  }
}
```
- An input that doesn’t induce a failure:

```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test 
  public void testReversed() {
    int[] input1 = {0,0};
    assertArrayEquals(new int[]{0,0}, ArrayExamples.reversed(input1));
  }
}
```
- Before fix:
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
- After fix: 
```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[arr.length - i - 1] = arr[i];
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```
