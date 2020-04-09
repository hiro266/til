# 画像挿入時のバグ修正

- image_tagの引数にnilが入るとエラーを吐く  
if(unless)でnil以外の時だけ画像を表示させてやれば良い
