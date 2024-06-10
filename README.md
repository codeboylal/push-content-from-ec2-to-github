# Pushing Code from EC2 to GitHub

Follow these steps to set up Git on your EC2 instance and push your code to GitHub.

## Steps:

1. **Connect to Your EC2 Instance**
    ```sh
    ssh -i /path/to/your-key-pair.pem ec2-user@your-ec2-instance-public-dns
    ```

2. **Install Git**
    ```sh
    # For Amazon Linux
    sudo yum update -y && sudo yum install git -y

    # For Ubuntu
    sudo apt-get update -y && sudo apt-get install git -y
    ```

3. **Configure Git**
    ```sh
    git config --global user.name "Your Name"
    git config --global user.email "your-email@example.com"
    ```

4. **Generate SSH Key**
    ```sh
    ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
    ```
    Follow the prompts to save the key and set a passphrase if desired.

5. **Add SSH Key to GitHub**
    ```sh
    cat ~/.ssh/id_rsa.pub
    ```
    Copy the output, then go to **GitHub** > **Settings** > **SSH and GPG keys** > **New SSH key**, paste the key, and give it a title.

6. **Verify SSH Connection**
    ```sh
    ssh -T git@github.com
    ```
    You should see a success message.

7. **Clone a Repository (if you have an existing repository)**
    ```sh
    git clone git@github.com:your-username/your-repository.git
    cd your-repository
    ```

8. **Create a New Repository (if creating a new repository)**
    1. On GitHub, create a new repository.
    2. Initialize a local Git repository and add the remote:
        ```sh
        mkdir your-repository
        cd your-repository
        git init
        git remote add origin git@github.com:your-username/your-repository.git
        ```

9. **Add, Commit, and Push Changes**
    ```sh
    git add .
    git commit -m "Your commit message"
    git push -u origin main  # Use 'master' if the default branch is named 'master'
    ```

10. **Optional: Set Up SSH Agent**
    ```sh
    # Start the ssh-agent in the background
    eval "$(ssh-agent -s)"
    # Add your SSH private key to the ssh-agent
    ssh-add ~/.ssh/id_rsa
    ```

By following these steps, you can successfully push code from your EC2 instance to your GitHub repository.
