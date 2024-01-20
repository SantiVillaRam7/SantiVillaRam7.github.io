---
title: "Graficar Anscombe"
output:
  html_document: default
  pdf_document: default
date: "2022-12-23"
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

Veamos el dataset y sus estadísticas para verificar resultados:

```{r anscombe, echo=TRUE}
head(anscombe,3)
miX <-anscombe[,1]
miY <-anscombe[,5]
mean(miX); mean(miY);
cor(miX,miY);
```
Ahora graficamos los puntos junto con una regresión lineal

```{r}
plot(miX,miY,col="blue",pch=19,xlim=c(3,19),ylim=c(3,13))
abline(lm(miY~miX),col="orange",lwd=3)
```

Este es el código para hacerlo en loops:

```{r}

ff <- y ~ x
mods <- setNames(as.list(1:4), paste0("lm", 1:4))
for(i in 1:4) {
  ff[2:3] <- lapply(paste0(c("y","x"), i), as.name)
  ## or   ff[[2]] <- as.name(paste0("y", i))
  ##      ff[[3]] <- as.name(paste0("x", i))
  mods[[i]] <- lmi <- lm(ff, data = anscombe)
  # print(anova(lmi))
}

op <- par(mfrow = c(2, 2), mar = 0.1+c(4,4,1,1), oma =  c(0, 0, 2, 0))
for(i in 1:4) {
  ff[2:3] <- lapply(paste0(c("y","x"), i), as.name)
  plot(ff, data = anscombe, col = "blue", pch = 19, cex = 1.2,
       xlim = c(3, 19), ylim = c(3, 13))
  abline(mods[[i]], col = "orange")
}
par(op)
```
