{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "colab": {
      "provenance": [],
      "authorship_tag": "ABX9TyPCjJzF2TSEVQcufNoe8Y4N",
      "include_colab_link": true
    },
    "kernelspec": {
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "name": "python"
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/jiq-star/UTS-DATMN-2304020029/blob/main/README.md\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "source": [
        "**Prediksi Kualitas Wine Menggunakan Model Klasifikasi**"
      ],
      "metadata": {
        "id": "XMX0VkWGLe1v"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Konteks"
      ],
      "metadata": {
        "id": "lbUG8bPNLymO"
      }
    },
    {
      "cell_type": "markdown",
      "source": [
        "Dalam industri wine, kualitas produk menjadi salah satu faktor penting yang dapat memengaruhi kepuasan konsumen dan nilai jual produk. Kualitas wine dapat dipengaruhi oleh berbagai karakteristik kimia, seperti tingkat keasaman, kadar alkohol, pH, kandungan sulfur dioxide, sulphates, dan beberapa faktor lainnya.\n",
        "\n",
        "Penilaian kualitas wine secara manual dapat membutuhkan waktu dan bergantung pada subjektivitas penilai. Oleh karena itu, pendekatan berbasis machine learning dapat digunakan untuk membantu memprediksi kualitas wine secara lebih cepat dan konsisten berdasarkan data karakteristik kimia yang tersedia."
      ],
      "metadata": {
        "id": "lHlbMHvcLzqU"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "import pandas as pd\n",
        "import joblib\n",
        "\n",
        "from sklearn.preprocessing import StandardScaler\n",
        "from sklearn.ensemble import RandomForestClassifier\n",
        "from sklearn.metrics import accuracy_score, confusion_matrix, classification_report"
      ],
      "metadata": {
        "id": "L0CA-_fqMcdz"
      },
      "execution_count": 1,
      "outputs": []
    }
  ]
}