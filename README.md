class DiagnosisAgent:
    def proses(self, pesan):
        pesan = pesan.lower()

        if "panas" in pesan or "overheat" in pesan:
            return "Komputer kemungkinan mengalami masalah pendinginan."

        elif "lambat" in pesan or "lemot" in pesan:
            return "Komputer kemungkinan mengalami beban sistem tinggi."

        elif "mati" in pesan or "tidak menyala" in pesan:
            return "Komputer kemungkinan mengalami masalah daya."

        else:
            return "Penyebab masalah belum diketahui."


class RecommendationAgent:
    def proses(self, diagnosis):
        if "pendinginan" in diagnosis:
            return "Periksa kipas dan ventilasi komputer."
        elif "beban sistem" in diagnosis:
            return "Periksa penggunaan CPU dan RAM."
        elif "masalah daya" in diagnosis:
            return "Periksa kabel dan sumber daya komputer."
        else:
            return "Periksa gejala lain untuk diagnosis lanjutan."


class RouterAgent:
    def _init_(self):
        self.diagnosis_agent = DiagnosisAgent()
        self.recommendation_agent = RecommendationAgent()

    def proses(self, pesan):
        print("\n[Router Agent] Menerima laporan masalah.")

        diagnosis = self.diagnosis_agent.proses(pesan)
        print("[Diagnosis Agent]", diagnosis)

        rekomendasi = self.recommendation_agent.proses(diagnosis)
        print("[Recommendation Agent]", rekomendasi)


def main():
    print("=== MULTI-AGENT SYSTEM ===")
    pesan = input("Jelaskan masalah komputer: ").strip()

    if pesan == "":
        print("Input tidak boleh kosong.")
        return

    router = RouterAgent()
    router.proses(pesan)


if _name_ == "_main_":
    main()
