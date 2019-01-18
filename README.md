# cryptool
Bash Powered OpenSSL Wrapper for Simple Enc/De/Cryption


**Usage**

    $ ./cryptool -h
     _____                      _                  _ 
    /  __ \                    | |                | |
    | /  \/ _ __  _   _  _ __  | |_   ___    ___  | |
    | |    | '__|| | | || '_ \ | __| / _ \  / _ \ | |
    | \__/\| |   | |_| || |_) || |_ | (_) || (_) || |
     \____/|_|    \__, || .__/  \__| \___/  \___/ |_|
                   __/ || |                          
                  |___/ |_|                          
                                                 

     Simple OpenSSL AES Enc/De/Crypt Tool

    -----------------------------------------------

    Encrypt a file/string with AES-128-CBC w/ Base64  

    -----------------------------------------------

    Usage: ./cryptool <-e/--encrypt>|<-d/--decrypt> 
        encrypt a file or string: ./cryptool -e <string/file> <passphrase>
        decrypt a file pr string: ./cryptool -d <string/file> <passphrase>

**Example:**

*Encrypt & Decrypt a string:*

    $ ./cryptool -e 'this is some data, eh' this_pass_phrase_is_at_LEAST_20_characters_LONG
    U2FsdGVkX19O0cni+Mki2RNQfT3WqLX/pVUWAISCyH5MEe7q0bIO3XbqD/WlhYw6
    $ ./cryptool -d 'U2FsdGVkX19O0cni+Mki2RNQfT3WqLX/pVUWAISCyH5MEe7q0bIO3XbqD/WlhYw6' this_pass_phrase_is_at_LEAST_20_characters_LONG
    this is some data, eh
    $
     
*Encrypt & Decrypt a file:*

    $ echo 'this is some data' >/tmp/a
    $ ./cryptool -e /tmp/a this_pass_phrase_is_at_LEAST_20_characters_LONG >/tmp/b
    $ ./cryptool -d /tmp/b this_pass_phrase_is_at_LEAST_20_characters_LONG
    this is some data
    $





**As a bashrc function**

Add these two functions to you ~/.bashrc file:

    enc(){
      case $1 in
      -h|--help) echo "Encrypt a file/string with AES-128-CBC w/ Base64 "
                 echo "                   enc <string> <password>"
                 echo "                   enc <file> <password>  "
      ;;

      *)
      test -f "$1" && is_File=true || is_File=false
      if $is_File; then
        cat "$1" | openssl enc -base64 -aes-128-cbc -a -salt -pass pass:"$2"
      else
        echo "$1" | openssl enc -base64 -aes-128-cbc -a -salt -pass pass:"$2"
      fi
      ;;
      esac
    }
    
    dec(){
      case $1 in
      -h|--help) echo  "Decrypt a file/string with AES-128-CBC w/ Base64 "
                 echo   "                  dec <string> <password>"
                 echo   "                  dec <file> <password>"

      ;;

      *)
      test -f "$1" && is_File=true || is_File=false
      if $is_File; then
        cat "$1" | openssl enc -d -base64 -aes-128-cbc -a -salt -pass pass:"$2"
      else
        echo "$1" | openssl enc -d -base64 -aes-128-cbc -a -salt -pass pass:"$2"
      fi
      ;;
      esac
    }


Then you can just call $ enc 'some data' some20characterormorepassphrase




**Like This Program? Tips are appreciated(!)**

BTC:1F48WFsbCBGuYCopXnBaK9tM7A2JhAWEyw
