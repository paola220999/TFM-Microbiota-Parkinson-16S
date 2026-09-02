# TFM-Microbiota-Parkinson-16S
Código de R y pipeline bioinformático para el re-análisis de la microbiota intestinal en la Enfermedad de Parkinson (BioProject PRJNA601994).
# ==============================================================================
# PIPELINE DE ANÁLISIS ESTADÍSTICO DE MICROBIOTA INTESTINAL EN PARKINSON (16S)
# Autor: Joseline Lucero
# Proyecto: TFM Microbiota y Enfermedad de Parkinson (PRJNA601994)
# ==============================================================================

# 1. CARGA DE LIBRERÍAS
library(phyloseq)
library(microbiome)
library(vegan)
library(ggplot2)
library(dplyr)

# 2. CARGA Y PREPARACIÓN DE DATOS
# Importación del objeto phyloseq generado desde QIIME2/SILVA v138.2
# ps <- readRDS("phyloseq_object.rds")

# 3. ANÁLISIS DE DIVERSIDAD ALFA
# Cálculo de Índices: Riqueza (Observed), Shannon y Pielou (Evenness)
# alpha_div <- estimate_richness(ps, measures = c("Observed", "Shannon"))
# alpha_div$Pielou <- evenness(ps, index = "pielou")$pielou

# Visualización con ggplot2
# plot_richness(ps, x = "Group", measures = c("Observed", "Shannon")) + 
#   geom_boxplot(aes(fill = Group)) + theme_bw()

# Test de Mann-Whitney / Wilcoxon para Diversidad Alfa
# wilcox.test(Shannon ~ Group, data = sample_data(ps))

# 4. ANÁLISIS DE DIVERSIDAD BETA (Multivariante)
# 4.1. Distancia de Bray-Curtis sobre Abundancias Relativas
# ps_rel <- transform_sample_counts(ps, function(x) x / sum(x))
# ord_pcoa_bray <- ordinate(ps_rel, method = "PCoA", distance = "bray")
# ord_nmds_bray <- ordinate(ps_rel, method = "NMDS", distance = "bray")

# PERMANOVA (Bray-Curtis)
# dist_bray <- phyloseq::distance(ps_rel, method = "bray")
# adonis2(dist_bray ~ Group, data = data.frame(sample_data(ps_rel)), permutations = 999)

# 4.2. Transformación CLR y Distancia de Aitchison
# ps_clr <- microbiome::transform(ps, transform = "clr")
# ord_pcoa_aitchison <- ordinate(ps_clr, method = "PCoA", distance = "euclidean")
# ord_nmds_aitchison <- ordinate(ps_clr, method = "NMDS", distance = "euclidean")

# PERMANOVA (Aitchison / CLR)
# dist_aitchison <- phyloseq::distance(ps_clr, method = "euclidean")
# adonis2(dist_aitchison ~ Group, data = data.frame(sample_data(ps_clr)), permutations = 999)

# 5. ABUNDANCIA DIFERENCIAL (Kruskal-Wallis con ajuste FDR)
# kw_results <- apply(otu_table(ps), 1, function(x) kruskal.test(x ~ sample_data(ps)$Group)$p.value)
# adj_p_values <- p.adjust(kw_results, method = "BH")
