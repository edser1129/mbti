import streamlit as st
import pandas as pd
import altair as alt

# 제목
st.title("국가별 MBTI 유형 분포 Top 10")

# CSV 파일 업로드
uploaded_file = st.file_uploader("CSV 파일을 업로드하세요", type=["csv"])

if uploaded_file is not None:
    # 데이터 불러오기
    df = pd.read_csv(uploaded_file)

    # MBTI 유형 리스트 (Country 제외)
    mbti_types = [col for col in df.columns if col != "Country"]

    # 사용자 선택 (드롭다운)
    selected_mbti = st.selectbox("MBTI 유형을 선택하세요:", mbti_types)

    # 선택된 MBTI 기준 Top 10 국가
    top10 = df[["Country", selected_mbti]].nlargest(10, selected_mbti)

    # Altair 그래프
    chart = (
        alt.Chart(top10)
        .mark_bar()
        .encode(
            x=alt.X(selected_mbti, title="비율"),
            y=alt.Y("Country", sort="-x", title="국가"),
            tooltip=["Country", selected_mbti]
        )
        .properties(
            width=600,
            height=400,
            title=f"{selected_mbti} 비율이 높은 국가 Top 10"
        )
        .interactive()
    )

    st.altair_chart(chart, use_container_width=True)

else:
    st.info("MBTI 국가별 분포 CSV 파일을 업로드해주세요.")
