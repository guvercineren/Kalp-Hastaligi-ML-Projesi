import streamlit as st

st.set_page_config(page_title="Kalp Hastalığı Risk Analizi", layout="centered")

st.title("🫀 Kalp Hastalığı Risk Analizi")
st.markdown("**Bulanık Üç Değerli Mantık (Fuzzy Three-Valued Logic) Karar Destek Sistemi**")
st.write("Lütfen risk analizi için aşağıdaki bilgileri doldurun:")

# Kullanıcı Girdileri
col1, col2 = st.columns(2)
with col1:
    gender = st.selectbox("Cinsiyetiniz", ["Kadın", "Erkek"])
with col2:
    age = st.number_input("Yaşınız", min_value=1, max_value=120, value=50)

st.subheader("Yaşam Tarzı Faktörleri")
smoke = st.radio("Sigara kullanıyor musunuz?", ["Hayır", "Evet"], horizontal=True)
alco = st.radio("Alkol kullanıyor musunuz?", ["Hayır", "Evet"], horizontal=True)
active = st.radio("Düzenli fiziksel aktivite yapıyor musunuz?", ["Hayır", "Evet"], horizontal=True)

if st.button("Riski Hesapla", type="primary"):
    # 1. Veri Dönüşümü (Binary'den Fuzzy formatına)
    x = 1 if smoke == "Evet" else 0
    y = 1 if alco == "Evet" else 0
    z_neg = 0 if active == "Evet" else 1

    # 2. Other Factors (Diğer Faktörler) Hesaplanması (Denklem 1)
    if x == 0 and y == 0 and z_neg == 0:
        other_factors = 0.0
    elif x == 1 and y == 1 and z_neg == 1:
        other_factors = 1.0
    else:
        other_factors = 0.5

    # 3. Makaledeki 12 Kuralın Uygulanması (Tablo 13)
    risk = ""
    
    if gender == "Kadın":
        if age < 55:
            if other_factors == 0.0: risk = "Risk Yok (0)"
            elif other_factors == 0.5: risk = "Risk Olabilir (0.5)"
            elif other_factors == 1.0: risk = "Risk Var (1)"
        else: # Kadın ve Yaş >= 55
            if other_factors == 0.0: risk = "Risk Olabilir (0.5)"
            elif other_factors == 0.5: risk = "Risk Olabilir (0.5)"
            elif other_factors == 1.0: risk = "Risk Var (1)"
            
    elif gender == "Erkek":
        if age < 45:
            if other_factors == 0.0: risk = "Risk Yok (0)"
            elif other_factors == 0.5: risk = "Risk Olabilir (0.5)"
            elif other_factors == 1.0: risk = "Risk Var (1)"
        else: # Erkek ve Yaş >= 45
            if other_factors == 0.0: risk = "Risk Olabilir (0.5)"
            elif other_factors == 0.5: risk = "Risk Olabilir (0.5)"
            elif other_factors == 1.0: risk = "Risk Var (1)"

    # Sonucu Ekrana Yazdırma
    st.markdown("---")
    st.subheader("Tahmin Sonucu")
    
    if "Yok" in risk:
        st.success(f"✅ **{risk}**: Harika! Davranışsal risk faktörlerinden uzaksınız.")
    elif "Olabilir" in risk:
        st.warning(f"⚠️ **{risk}**: Dikkat! Risk gelişimi olabilir. Eksik olan sağlıklı yaşam faktörlerini rutininize eklemelisiniz.")
    else:
        st.error(f"🚨 **{risk}**: Risk faktörleri mevcut! Lütfen sağlığınıza dikkat edip bir uzmana başvurun.")
