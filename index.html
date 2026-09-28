# ============================================================
#  ☁️ MAKTAB BUXGALTERIYA CLOUD — PYTHON VERSIYA
# ============================================================
#  Texnologiya: Python + Streamlit + Firebase (REST API)
#  Ishga tushirish:  streamlit run buxgalteriya.py
#
#  ✅ Bitta fayl — HTML/CSS/JS umuman yo'q!
#  ✅ Bulut: eski versiyadagi ma'lumotlar ham ko'rinadi
#  ✅ Streamlit Cloud'da requirements.txt shart emas
# ============================================================

import io
from datetime import datetime

import pandas as pd
import requests
import streamlit as st

# ---------------- ASOSIY SOZLAMALAR ----------------
DB_URL = "https://maktab-buxgalteriya-default-rtdb.firebaseio.com"
OYLAR = ["Yanvar", "Fevral", "Mart", "Aprel", "May", "Iyun",
         "Iyul", "Avgust", "Sentabr", "Oktabr", "Noyabr", "Dekabr"]
STANDART_LOGIN = "admin"
STANDART_PAROL = "123"

ST_MAP = {"QARZ": "st-debt", "QISMAN": "st-partial", "TO'LANDI": "st-paid"}
ST_BACK = {v: k for k, v in ST_MAP.items()}

st.set_page_config(page_title="Maktab Buxgalteriya", page_icon="☁️", layout="wide")

# ---------------- BULUT FUNKSIYALARI ----------------

def bulutdan_ol(yol):
    """Firebase'dan ma'lumot o'qiydi (REST API orqali)"""
    try:
        r = requests.get(f"{DB_URL}/{yol}.json", timeout=8)
        if r.status_code == 200:
            return r.json()
    except Exception:
        pass
    return None

def bulutga_yoz(qiymat):
    """Firebase'ga ma'lumot yozadi"""
    try:
        r = requests.put(f"{DB_URL}/accounting/data.json", json=qiymat, timeout=8)
        return r.status_code == 200
    except Exception:
        return False

def telegramga_yubor(token, chat_id, matn):
    try:
        r = requests.post(f"https://api.telegram.org/bot{token}/sendMessage",
                          json={"chat_id": chat_id, "text": matn, "parse_mode": "HTML"},
                          timeout=8)
        return r.ok
    except Exception:
        return False

# ---------------- JADVAL YORDAMCHILARI ----------------

def df_yasa(oy):
    """Bulutdagi ma'lumotni jadval (DataFrame) ko'rinishiga keltiradi"""
    royxat = st.session_state.data.get(oy) or []
    qatorlar = [{
        "name": str(s.get("name") or ""),
        "price": float(s.get("price") or 0),
        "food": float(s.get("food") or 0),
        "st": ST_BACK.get(s.get("st") or "st-debt", "QARZ"),
        "att": bool(s.get("att", True)),
    } for s in royxat]
    return pd.DataFrame(qatorlar, columns=["name", "price", "food", "st", "att"])

def toza_df(df):
    """Bo'sh katakchalarni to'ldiradi (bulutga yozishdan oldin majburiy!)"""
    df = df.copy()
    df["name"] = df["name"].fillna("")
    df["price"] = df["price"].fillna(0)
    df["food"] = df["food"].fillna(0)
    df["st"] = df["st"].fillna("QARZ").map(ST_MAP)
    df["att"] = df["att"].fillna(True).astype(bool)
    return df

# ---------------- SESSION HOLAT ----------------
if "kirgan" not in st.session_state:
    st.session_state.kirgan = False
    st.session_state.data = {}
    st.session_state.versiya = 0
    st.session_state.yuklandi = False

# ---------------- KIRISH OYNASI ----------------
cfg = bulutdan_ol("accounting/config") or {}
LOGIN = cfg.get("user") or STANDART_LOGIN
PAROL = cfg.get("pass") or STANDART_PAROL

if not st.session_state.kirgan:
    st.markdown("## ☁️ Cloud Buxgalteriya (Python)")
    _, c, _ = st.columns([1, 2, 1])
    with c:
        u = st.text_input("Login")
        p = st.text_input("Parol", type="password")
        if st.button("🔑 Kirish", use_container_width=True):
            if u.strip() == LOGIN and p == PAROL:
                st.session_state.kirgan = True
                st.rerun()
            else:
                st.error("Login yoki parol xato!")
        with st.expander("❓ Parolni unutdim"):
            tel = st.text_input("Telefon raqamingiz (+998...)")
            if st.button("Parolni ko'rish"):
                if tel.strip() and tel.strip() == (cfg.get("phone") or ""):
                    st.info(f"Login: {LOGIN} | Parol: {PAROL}")
                else:
                    st.error("Bu telefon raqam ro'yxatda yo'q!")
    st.stop()

# ---------------- BULUTDAN YUKLASH ----------------
if not st.session_state.yuklandi:
    st.session_state.data = bulutdan_ol("accounting/data") or {}
    st.session_state.yuklandi = True

# ---------------- SARLAVHA ----------------
s1, s2 = st.columns([3, 1])
with s1:
    st.markdown("## Maktab Pro ☁️ — Python versiya")
with s2:
    if st.button("🔄 Bulutdan yangilash"):
        st.session_state.data = bulutdan_ol("accounting/data") or {}
        st.session_state.versiya += 1
        st.rerun()

# ---------------- OY TANLASH ----------------
oy = st.selectbox("📅 Oy", OYLAR, index=datetime.now().month - 1)

# ---------------- JADVAL (TAXRIRLANADIGAN) ----------------
st.caption("✏️ Jadvalni to'g'ridan-to'g'ri tahrirlang. Pastdagi «+» belgisi orqali "
           "yangi o'quvchi qo'shing. O'chirish uchun qator boshidagi kutbxonani bosing.")

tahrirlangan = st.data_editor(
    df_yasa(oy),
    column_config={
        "name": st.column_config.TextColumn("👤 Ism Sharif", width="large"),
        "price": st.column_config.NumberColumn("💰 Narx", step=1000),
        "food": st.column_config.NumberColumn("🍽 Ovqat", step=1000),
        "st": st.column_config.SelectboxColumn("Holat",
             options=["QARZ", "QISMAN", "TO'LANDI"], default="QARZ"),
        "att": st.column_config.CheckboxColumn("✅ Darsga keldi", default=True),
    },
    num_rows="dynamic",
    hide_index=True,
    use_container_width=True,
    key=f"jadval_{oy}_{st.session_state.versiya}",
)

# ---------------- TUGMALAR ----------------
b1, b2, b3, b4 = st.columns(4)

with b1:
    if st.button("💾 Bulutga saqlash", type="primary", use_container_width=True):
        st.session_state.data[oy] = toza_df(tahrirlangan).to_dict("records")
        if bulutga_yoz(st.session_state.data):
            st.success("✅ Saqlandi!")
        else:
            st.error("⚠️ Bulutga yozib bo'lmadi — internetni tekshiring!")

with b2:
    if st.button("📋 O'tgan oydan ko'chirish", use_container_width=True):
        idx = OYLAR.index(oy)
        if idx == 0:
            st.warning("Yanvardan oldingi oy yo'q!")
        else:
            prev = st.session_state.data.get(OYLAR[idx - 1]) or []
            if not prev:
                st.warning(f"{OYLAR[idx-1]} oyida ma'lumot yo'q!")
            else:
                st.session_state.data[oy] = [
                    {**dict(s), "st": "st-debt", "att": True} for s in prev
                ]
                if bulutga_yoz(st.session_state.data):
                    st.session_state.versiya += 1
                    st.success("Ko'chirildi ✅")
                    st.rerun()

with b3:
    toza = toza_df(tahrirlangan)
    excel_buf = io.BytesIO()
    excel_tayyor = False
    try:
        with pd.ExcelWriter(excel_buf, engine="openpyxl") as w:
            toza.rename(columns={
                "name": "Ism Sharif", "price": "Narx", "food": "Ovqat",
                "st": "Holat", "att": "Davomat"}).to_excel(w, index=False, sheet_name=oy)
        excel_tayyor = True
    except Exception:
        pass
    if excel_tayyor:
        st.download_button("📊 Excel yuklab olish", excel_buf.getvalue(),
                           file_name=f"Hisobot_{oy}.xlsx", use_container_width=True)
    else:
        csv = toza.to_csv(index=False).encode("utf-8-sig")
        st.download_button("📊 CSV yuklab olish", csv,
                           file_name=f"Hisobot_{oy}.csv", use_container_width=True)

with b4:
    if st.button("🤖 Telegramga yuborish", use_container_width=True):
        if not cfg.get("tgToken") or not cfg.get("chatId"):
            st.error("Firebase'dagi config'ga Bot Token va Chat ID kiriting!")
        elif toza.empty:
            st.warning("Ma'lumot yo'q!")
        else:
            matn = f"📊 <b>{oy} oyi hisoboti</b>\n\n"
            for i, s in toza.iterrows():
                belgi = "✅" if s["st"] == "st-paid" else "🟡" if s["st"] == "st-partial" else "🔴"
                matn += f"{i+1}. <b>{s['name']}</b> — {int(s['price']):,} so'm {belgi}\n".replace(",", " ")
            matn += f"\n💰 Jami tushum: <b>{int(toza['price'].sum()):,} so'm</b>".replace(",", " ")
            if telegramga_yubor(cfg["tgToken"], cfg["chatId"], matn):
                st.success("Telegramga yuborildi! 🤖")
            else:
                st.error("Yuborib bo'lmadi — token/chat ID'ni tekshiring!")

# ---------------- STATISTIKA ----------------
st.markdown("---")

if toza.empty:
    tushum = chiqim = foyda = qarz = 0
    dav_foiz = 0
else:
    tushum = float(toza["price"].sum())
    chiqim = float(toza["food"].sum())
    foyda = tushum - chiqim
    qarzdorlar = toza[toza["st"] == "st-debt"]
    qarz = float((qarzdorlar["price"] - qarzdorlar["food"]).sum())
    dav_foiz = round(float(toza["att"].mean()) * 100)

m1, m2, m3, m4, m5, m6 = st.columns(6)
m1.metric("💰 Tushum", f"{int(tushum):,} so'm".replace(",", " "))
m2.metric("🍽 Chiqim", f"{int(chiqim):,} so'm".replace(",", " "))
m3.metric("✅ Foyda", f"{int(foyda):,} so'm".replace(",", " "))
m4.metric("👥 O'quvchi", len(toza))
m5.metric("📅 Davomat", f"{dav_foiz}%")
m6.metric("🔴 Qarz", f"{int(qarz):,} so'm".replace(",", " "))

# ---------------- GRAFIK ----------------
st.markdown("---")
st.bar_chart(pd.DataFrame(
    {"so'm": [tushum, chiqim, foyda]},
    index=["Tushum", "Chiqim", "Foyda"]),
    color=["#6366f1"])

st.caption("Python + Streamlit bilan yozilgan 💛 | Login: " + LOGIN)
