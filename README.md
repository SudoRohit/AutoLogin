# AutoLogin using Selenium

## Method 1 - Using Selenium IDE

You need to add Selenium IDE Extension to your browser.

![Screenshot from 2022-10-12 15-03-23](https://user-images.githubusercontent.com/54389006/195306955-180d49df-64f7-46bc-b60e-377f594342d9.png)


Open the extension and click on record button to record the actions which you want to automate and then save the file. Your automation is ready. Now you can run the automation whenever you want.

![Screenshot from 2022-10-12 15-16-42](https://user-images.githubusercontent.com/54389006/195310164-c93bc1b2-5183-4e58-87bd-8f7a5bcdd7ad.png)


You can also insert the commands manually.

## Method 2 - Using Selenium Web Driver

You can use various languages to use selenium. Here we will be using python.

You need to install selenium package. You can use pip to install the package.

```
pip install -U selenium
```

Then you need to download the web driver for your browser. Here we used Firefox browser, so we downloaded Gecko Driver.

Now open any text editor and type your code.

#### Following is the code for automating login page.

```
from selenium import webdriver
from selenium.webdriver.firefox.service import Service
from selenium.webdriver.common.by import By


class Browser:
    browser, service = None, None

    def __init__(self, driver: str):
        self.service = Service(driver)
        self.browser = webdriver.Firefox(service=self.service)

    def open_page(self, url: str):
        self.browser.get(url)

    def add_input(self, by: By, value: str, text: str):
        field = self.browser.find_element(by=by, value=value)
        field.send_keys(text)

    def click_button(self, by: By, value: str):
        button = self.browser.find_element(by=by, value=value)
        button.click()

    def login(self, username: str, password: str):
        self.add_input(by=By.ID, value='login_email', text=username)
        self.add_input(by=By.ID, value='login_password', text=password)
        self.click_button(by=By.CLASS_NAME, value='btn-login')


if __name__ == '__main__':
    browser = Browser('./geckodriver')

    browser.open_page('https://gne2.gndec.ac.in/login#login')

    browser.login(username='USERNAME', password='PASSWORD')
```

Run the code to perform your automation.
