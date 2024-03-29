---
title: "Tarea Anscombe"
---
Segundo dataset:
```{r setup, include=FALSE}
plot(anscombe$x2, anscombe$y2, main = "Segundo conjunto", pch = 19)
abline(lm(miY~miX),col="orange",lwd=3)
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
