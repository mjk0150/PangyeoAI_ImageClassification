※ 코드 구성:
- 주요 버전, 라이브러리 정보
- 라이브러리 호출 및 I/O
- Argument Setting
- DataLoader 
- Model
- SAM Optimizer w. AdamP
- SAM Trainer
- Metrics
- Misc.
- 학습 Function
- Train and Infer

※ 환경 구성
cwd: './'
subdirectories:
  './train'
    './train/Mask'
    './train/NoMask'
  './test'
  './weights'
  './results'

※ 코드 동작, 결과 재현:
라이브러리 호출 및 I/O 부터 쭉 실행시켜주시면,
'./results/mask_pred_with_dm_nfnet_f2_SAM_AdamP_AA.csv' 에 결과가 저장되고,
'./weights/dm_nfnet_f2_SAM_AdamP_AA_best.pt' 에 모델 파일이 저장됩니다.

*코드 내에 에러 문구가 있는데 다시 돌리시면 문제 없이 재현됩니다!!

※ 코드 구성 상세():
- 주요 버전, 라이브러리 정보:
	- torch, torchvision, opencv 만 정리했습니다.
	  torch: 1.9.0
	  torchvision: 0.10.0
	  cv2: 4.5.2  

- 라이브러리 호출 및 I/O
	- timm, adamp 는 따로 설치를 해주어야 하며, 
	  pip install git+https://github.com/rwightman/pytorch-image-models.git
	  pip install adamp
	  로 설정해주시면 되겠습니다.

- Argument Setting
	- directory/path 설정 및, hyperparameter 설정

- DataLoader 
	- train / test dataset --> dataloader

- Model
	- timm 에서 df_nfnet을 불러와서 쓸 수 있도록 NFNMaskClassifier 정의

- SAM Optimizer w. AdamP
	- SAM optimization 정의

- SAM Trainer
	- 베이스라인 Trainer() 을 SAM optimization에 맞게 수정

- Metrics
	- 베이스라인 코드

- Misc.
	- 결과 확인 및 쿠다 메모리 관리용

- 학습 Function
	- model, optimizer, learning rate scheduler, criterion을 다 선언해주고, SAM Trainer로 학습한 후에 이어서 testdataloader로 추론까지 하도록 정의.

- Train and Infer
	- NFN_train_val_infer() 안에 모델명만 넣어서 학습-추론 실행


※이상 ★참치김치찌개★ 팀이였습니다. 좋은 대회 열어주셔서 감사합니다!!※