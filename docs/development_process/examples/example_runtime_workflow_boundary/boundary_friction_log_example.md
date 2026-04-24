# Boundary Friction Log

記入方針: 不快感のメモではなく、どの境界で何が摩擦になっているかを具体化します。

## Date

2026-04-24

## Area

app / runtime boundary around post-turn control

## Friction summary

turn 実行後の次アクション判断が app-local と trace assembly で二重に扱われている。

## Observed symptom

worker が stop / continue の扱いを変更すると、trace の説明と loop の挙動が一緒に壊れやすい。

## Suspected boundary

`app` と `runtime_protocol` の ownership boundary

## Affected consumer or workflow

- post-turn loop
- trace consumer
- closeout review

## Current evidence strength

中程度

## Why this is not yet a lane

blocked consumer は見え始めているが、まだ 1 本の lane に絞れるほど trigger が整理されていない。

## Recheck trigger

次の audit で、trace consumer と runtime loop の両方が concrete に困っているか確認する。
