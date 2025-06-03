# aedf]


코드 구현


import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

sns.set(font="Malgun Gothic", rc={"axes.unicode_minus": False})

df = pd.read_csv("subway_data.csv", encoding='euc-kr')  # 파일명은 실제 데이터에 맞게 수정
print("데이터 미리보기:")
print(df.head())

morning_df = df[df['시간대'].isin(['07:00~07:59', '08:00~08:59'])]
evening_df = df[df['시간대'].isin(['18:00~18:59', '19:00~19:59'])]

morning_exit = morning_df.groupby('하차역')['하차인원'].sum().sort_values(ascending=False)

evening_board = evening_df.groupby('승차역')['승차인원'].sum().sort_values(ascending=False)

evening_exit = evening_df.groupby('하차역')['하차인원'].sum().sort_values(ascending=False)

plt.figure(figsize=(10, 6))
morning_exit.head(10).plot(kind='bar', color='skyblue')
plt.title("출근 시간 하차 인원이 많은 역 (Top 10)")
plt.ylabel("하차 인원 수")
plt.xlabel("지하철역")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

plt.figure(figsize=(10, 6))
evening_board.head(10).plot(kind='bar', color='lightgreen')
plt.title("퇴근 시간 승차 인원이 많은 역 (Top 10)")
plt.ylabel("승차 인원 수")
plt.xlabel("지하철역")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

plt.figure(figsize=(10, 6))
evening_exit.head(10).plot(kind='bar', color='salmon')
plt.title("퇴근 시간 하차 인원이 많은 역 (Top 10)")
plt.ylabel("하차 인원 수")
plt.xlabel("지하철역")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()


<분석>

1.데이터를 시간대별로 나누어 출근(0709시) / 퇴근(1820시)으로 나눔

2. 각 시간대의 승차/하차 인원을 역별로 합산

3. 가장 유동 인구가 많은 상위 역들을 시각화로 도출

4. 이를 바탕으로 출근역/퇴근역/주거역/업무지구 판단 가능
