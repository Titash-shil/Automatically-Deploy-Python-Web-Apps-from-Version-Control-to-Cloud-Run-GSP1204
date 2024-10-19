# Automatically Deploy Python Web Apps from Version Control to Cloud Run || [GSP1204](https://www.cloudskillsboost.google/focuses/80415?parent=catalog) ||

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

- **Prerequisites**

* If you do not already have a **GitHub** account, you will need to create a [GitHub account](https://github.com/signup)

- **Recommendations**

* Use an existing **GitHub** account if you have one. **GitHub** is more likely to block a new account as spam.

* Configure [two-factor authentication](https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication) on your GitHub account to reduce the chances of your account being marked as spam.

---

- ### Run the following Commands in CloudShell

```
gcloud services enable \
    cloudbuild.googleapis.com \
    run.googleapis.com

cd ~

mkdir helloworld

cd helloworld

cat > requirements.txt << "EOF"
Flask==3.0.0
gunicorn==20.1.0
EOF

touch main.py

cat > main.py <<EOF_END
import os

from flask import Flask

app = Flask(__name__)

app_version = "0.0.0"

@app.route("/")
def hello_world():
    return f"Hello! This is version {app_version} of my application."


if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0", port=int(os.environ.get("PORT", 8080)))
EOF_END

cd ~/helloworld

git init -b main

curl -sS https://webi.sh/gh | sh

gh auth login

gh api user -q ".login"

GITHUB_USERNAME=$(gh api user -q ".login")

echo ${GITHUB_USERNAME}

git config --global user.name "${GITHUB_USERNAME}"
git config --global user.email "${USER_EMAIL}"

git add .

git commit -m "initial commit"

cd ~/helloworld

gh repo create hello-world --private

git remote add origin \
https://github.com/${GITHUB_USERNAME}/hello-world

git push -u origin main

echo -e "\n\nTo see your code, visit this URL:\n \
https://github.com/${GITHUB_USERNAME}/hello-world/blob/main/main.py \n\n"
```

- Go to **Clod Run** from [here](https://console.cloud.google.com/run)

---

- ### Run again the following Commands in CloudShell

```
cd helloworld

cat > main.py <<EOF_END
import os

from flask import Flask

app = Flask(__name__)

app_version = "0.0.1"

@app.route("/")
def hello_world():
    return f"Hello! This is version {app_version} of my application."


if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0", port=int(os.environ.get("PORT", 8080)))
EOF_END

git add .
git commit -m "update version to 0.0.1"

git push

echo -e "\n\nTo see your code, visit this URL:\n \
https://github.com/${GITHUB_USERNAME}/hello-world/blob/main/main.py \n\n"

echo -e "\n\nOnce the build finishes, visit this URL to see your live application:\n \
"$(gcloud run services list | awk '/URL/{print $2}' | head -1)" \n\n"
```
---

# Congratulations ..!!🎉  You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)
