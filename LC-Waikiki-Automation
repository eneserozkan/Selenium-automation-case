import unittest
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.chrome.service import Service
import time

from selenium.webdriver.support.wait import WebDriverWait
from webdriver_manager.chrome import ChromeDriverManager


class Test_Check_LcWaikiki(unittest.TestCase):
    def setUp(self):
        self.driver = webdriver.Chrome(ChromeDriverManager().install())
        self.driver.maximize_window()
        self.driver.get("https://www.lcwaikiki.com/tr-TR/TR")
        self.driver.implicitly_wait(10)
        self.wait = WebDriverWait(self.driver, 10)

    def test_check_lcwaikiki(self):
        self.driver.find_element(By.XPATH, "//*[contains(text(),'KADIN')]").click()
        page_title = self.driver.title
        self.assertEqual("Kadın Giyim - Kadın Kıyafetleri - LC Waikiki", page_title)
        self.driver.find_element(By.LINK_TEXT, "Eşofman Altı").click()
        self.driver.find_element(By.XPATH, "//*[contains(text(),'Beli Lastikli Düz Kadın Jogger Eşofman Altı')]").click()
        product_page_title = self.driver.title
        self.assertTrue(product_page_title,
                        self.driver.find_element(By.XPATH, "//*[contains(text(),'Beli Lastikli Düz Kadın Jogger Eşofman Altı')]"))

        self.driver.find_element(By.ID, "pd_add_to_cart").click()
        text_trial = self.driver.find_element(By.ID, "pd_add_to_cart").text
        assert text_trial == "LÜTFEN BEDEN SEÇİNİZ", "Something seems wrong!"
        time.sleep(5)
        self.driver.find_element(By.XPATH, "//*[@id='option-size']/a[1]").click()
        self.driver.find_element(By.ID, "pd_add_to_cart").click()
        time.sleep(3)
        self.assertTrue("Sepetinize 1 adet ürün eklenmiştir.", self.driver.find_element(By.CLASS_NAME, "drop-down-menu__wrapper").text)
        self.driver.find_element(By.CSS_SELECTOR, ".cart-dropdown:nth-child(3)").click()
        self.assertIn("Sepetim", self.driver.find_element(By.CSS_SELECTOR, ".cart-dropdown:nth-child(3)").text)
        self.driver.find_element(By.CLASS_NAME, "main-header-logo").click()
        main_page = self.driver.title
        self.assertTrue("LC Waikiki | İlk Alışverişte Kargo Bedava! - LC Waikiki", main_page)

    def tearDown(self):
        self.driver.quit()
