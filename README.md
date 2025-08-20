# Viroma
Esse projeto foi feito no Google Colab.

Contextualização do exame
O exame de viroma, como discutido em aula, foi desenvolvido para a identificação de patógenos virais em amostras clinicas através da técnica de metagenômica. O fluxo do exame é constituido de uma etapa de wet-lab e uma etapa de bioinformática conforme figura abaixo. Nós focaremos na execução do pipeline de bioinformática e na interpretação dos seus resultados.

Neste notebook, nós iremos entender e executar cada um dos principais passos para execução do pipeline de viroma em amostras clínicas.
Input: FASTQ paired-end do sequenciamento da amostra.
Output: Relatórios de diversidade para análise e interpretação do analista.
Note que trouxemos aqui uma versão simplificada do pipeline, mas que traz a essência dos passos mais fundamentais da análise. Ao final da aula prática, pense em formas de melhorá-lo ou etapas adicionais que você poderia criar para trazer resultados mais interessantes.

<img width="1922" height="1038" alt="image" src="https://github.com/user-attachments/assets/e6d3d28e-7ce7-4300-8882-cd8212c7815f" />
<img width="1271" height="677" alt="image" src="https://github.com/user-attachments/assets/52573c88-9bc3-4afc-b04c-ed0462b12e0d" />


Descrição do caso
Escopo: Desde muito tempo a humanidade procurou conhecer quais eram os microrganismos que habitam o nosso planeta e principalmente as várias partes do nosso corpo. Historicamente, a presença de bactérias e vírus esteve relacionada com a presença de infecções de caráter patológico e o seu diagnóstico com técnicas dependentes de cultivo. Hoje, com a consolidação das técnicas de NGS e da metagenômica como área dentro da bioinformática, sabemos que existe uma grande maioria de microrganismos que não são cultiváveis e passaram despercebidos das nossas técnicas de identificação por todo este tempo. E as implicações da presença, ausência e abundância destes microrganismos no corpo humano só começaram a ser elucidadas. Considerando que os microrganismos são de uma diversidade genômica espantosa (diversidade de genes, tamanhos, organização genômica, RNA, DNA, etc.), somente o uso de técnicas ômicas diversas podem nos trazer informações da comunidade microbiana como um todo. Sendo assim, a análise em conjunto do patógeno primário de uma doença, das suas características genômicas, e dos demais microrganismos presentes na amostra podem trazer informações relevantes para entender o desfecho clínico de uma patologia.

Objetivo geral: Análise da comunidade microbiana presente na amostra através de técnicas ômicas e identificação de possíveis patógenos


#Material fornecido: 
#Dois pares de FASTQ gerados a partir de uma mesma amostra de um mesmo paciente, porém com execuções de laboratório e metodologias ômicas diferentes:
#- Viroma de RNA (Metatranscriptômica ou RNA total)
#VIROMA-R1: https://aulas-pos-hiae-public-data.s3.sa-east-1.amazonaws.com/TCC-metagenomica/patient_joao_VIROMA_S21_R1_001.fastq.gz
#VIROMA-R2: https://aulas-pos-hiae-public-data.s3.sa-east-1.amazonaws.com/TCC-metagenomica/patient_joao_VIROMA_S21_R2_001.fastq.gz

#- Microbioma (Amplicon 16S)
#MICROBIOMA-R1: https://aulas-pos-hiae-public-data.s3.sa-east-1.amazonaws.com/TCC-metagenomica/patient_joao_MICROBIOMA16S_S69_R1_001.fastq.gz
#MICROBIOMA-R2: https://aulas-pos-hiae-public-data.s3.sa-east-1.amazonaws.com/TCC-metagenomica/patient_joao_MICROBIOMA16S_S69_R2_001.fastq.gz

