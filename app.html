import os
import sqlite3
from PIL import Image
import streamlit as st

# إنشاء مجلد لحفظ الصور المرفوعة إذا لم يكن موجوداً
UPLOAD_DIR = "uploaded_images"
os.makedirs(UPLOAD_DIR, exist_ok=True)

# إعداد قاعدة البيانات
def init_db():
    conn = sqlite3.connect("archive.db")
    cursor = conn.cursor()
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS archive (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            name TEXT NOT NULL,
            image_path TEXT NOT NULL
        )
    """)
    conn.commit()
    conn.close()

init_db()

st.title("📁 برنامج الأرشيف الإلكتروني للأسماء والصور")

# الشريط الجانبي للإضافة
st.sidebar.header("إضافة سجل جديد")
name_input = st.sidebar.text_input("الاسم:")
uploaded_file = st.sidebar.file_uploader("اختر صورة:", type=["jpg", "png", "jpeg"])

if st.sidebar.button("حفظ في الأرشيف"):
    if name_input and uploaded_file:
        # حفظ الصورة محلياً
        image_path = os.path.join(UPLOAD_DIR, uploaded_file.name)
        with open(image_path, "wb") as f:
            f.write(uploaded_file.getbuffer())
        
        # حفظ البيانات في قاعدة البيانات
        conn = sqlite3.connect("archive.db")
        cursor = conn.cursor()
        cursor.execute("INSERT INTO archive (name, image_path) VALUES (?, ?)", (name_input, image_path))
        conn.commit()
        conn.close()
        
        st.sidebar.success(f"تم حفظ '{name_input}' بنجاح! ✅")
        st.rerun()  # إعادة تحميل الصفحة لتحديث العرض
    else:
        st.sidebar.error("الرجاء إدخال الاسم واختيار صورة.")

# --- قسم البحث ---
st.header("📋 الأرشيف الحالي")
search_query = st.text_input("🔍 ابحث بالاسم:", "")

# استرجاع البيانات بناءً على البحث
conn = sqlite3.connect("archive.db")
cursor = conn.cursor()

if search_query:
    cursor.execute("SELECT id, name, image_path FROM archive WHERE name LIKE ?", ('%' + search_query + '%',))
else:
    cursor.execute("SELECT id, name, image_path FROM archive")

records = cursor.fetchall()

if not records:
    st.info("لا توجد نتائج مطابقة في الأرشيف.")
else:
    for record_id, name, img_path in records:
        col1, col2, col3 = st.columns([1, 2, 1])
        
        with col1:
            if os.path.exists(img_path):
                img = Image.open(img_path)
                st.image(img, width=120)
            else:
                st.warning("الصورة غير موجودة")
                
        with col2:
            st.subheader(f"الاسم: {name}")
            st.text(f"المعرف (ID): {record_id}")
            
        with col3:
            # زر الحذف لكل سجل
            if st.button("🗑️ حذف", key=f"del_{record_id}"):
                # حذف الصورة من المجلد إذا كانت موجودة
                if os.path.exists(img_path):
                    os.remove(img_path)
                
                # حذف السجل من قاعدة البيانات
                cursor.execute("DELETE FROM archive WHERE id = ?", (record_id,))
                conn.commit()
                conn.close()
                
                st.success(f"تم حذف السجل بنجاح!")
                st.rerun()  # إعادة تحميل الصفحة لتحديث القائمة
                
        st.markdown("---")

conn.close()

