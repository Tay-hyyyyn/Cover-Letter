# Stacking ensemble(기존 27cell 30d41a5b953d809eb80cfcc12cec2dfe

# Stacking ensemble(기존 27cell

# 1. 앙상블에 필요한 추가 모듈 임포트

from sklearn.ensemble import RandomForestClassifier, StackingClassifier
from xgboost import XGBClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import Pipeline

# 2. 개별 모델(Base Models) 정의

# 디스커션의 ‘layer_0’ 들에 해당하는 각기 다른 특성의 모델들을 준비합니다.

model_lr = LogisticRegression(max_iter=1000, n_jobs=-1, random_state=42)

model_xgb = XGBClassifier(
n_estimators=200,
max_depth=5,
learning_rate=0.05,
random_state=42,
eval_metric=‘logloss’
)

model_rf = RandomForestClassifier(
n_estimators=200,
max_depth=5,
random_state=42,
n_jobs=-1
)

# 3. 스태킹 앙상블 모델 (Stacking Classifier) 생성

# 3개의 모델이 예측한 값들을 이어 붙여서(Concat), 최종 보스(final_estimator)가 한 번 더 학습합니다.

stacking_model = StackingClassifier(
estimators=[
(‘LR’, model_lr),
(‘XGB’, model_xgb),
(‘RF’, model_rf)],
final_estimator=LogisticRegression(), # 최종 결정은 안정적인 로지스틱 회귀가 내림
cv=5, # 5번 교차 검증을 통해 메타 모델을 견고하게 학습
n_jobs=-1
)

# 4. 기존 파이프라인에 스태킹 모델 결합

# 이전에 만들어둔 전처리 파이프라인(preprocessor) 뒤에 스태킹 모델을 연결합니다.

clf = Pipeline(
steps=[
(‘preprocess’, preprocessor),
(‘model’, stacking_model), # 기존의 단일 로지스틱 모델 대신 합체 로봇이 들어갑니다!]
)