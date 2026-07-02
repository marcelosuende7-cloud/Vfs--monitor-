# Vfs--monitor-
from playwright.sync_api import sync_playwright
import time

URL = "https://visa.vfsglobal.com/"

def verificar():
    with sync_playwright() as p:
        browser = p.chromium.launch(headless=True)

        page = browser.new_page()

        page.goto(URL)

        # Aguarde carregar
        page.wait_for_timeout(5000)

        texto = page.content()

        if "No appointment slots available" in texto:
            print("Sem vagas")

        elif "Available" in texto:
            print("VAGA ENCONTRADA!")

            # Aqui você envia Telegram ou email

        browser.close()

while True:
    verificar()
    time.sleep(300)  # verifica a cada 5 minutos
    
