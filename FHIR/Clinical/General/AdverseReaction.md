## AdverseReaction

물질에 대한 반응 대상의 노출과 관련이 있다고 예상되지 않은 반응을 기록합니다.(알러지 반응?)


### Scope and Usage

**AdverseReaction** 는 물질에 대한 특정 반응에 대한 정보를 제공하는 데 사용됩니다. 이들은 일반적으로 **AllergyIntolerance** 리소스와 관련이 있지만, 추가 반응이 없다거나 특정 이벤트가 설명 될 때 자체적으로보고 될 수 있습니다.


### Background and Context

**AdverseReaction** 은 일반적으로 증상 클래스에보고 된 일련의 징후 또는 증상을 가지고 있습니다. 그러나, 발생 된 특정 징후 또는 증상을 알지 않고 **AdverseReaction** 이 발생했다는 것을 전달하는 것이 가능하다. 일부 알려지지 않은 반응이 발생했습니다. 유사하게, 일련의 증상이있는 **AdverseReaction** 이 있었지만 그것이 알려지지 않았다면 물질을 나타내지는 않을 수 있음을 전달하는 것이 가능합니다. (예 : 어떤 알려지지 않은 이유로 발진이 일어났습니다.)

Exposure 클래스는 반응 이전의 노출 세트를 나타내는 데 사용됩니다. 인과 관계에 대한 주장은 없으며, 순전히 타이밍의 진술이다. 각 노출은 필요한 경우 반응과 다를 수있는 물질을 나타낼 수 있습니다.


### Format

#### AdverseReaction
- Definition: 물질에 대한 반응 대상의 노출과 관련이 있다고 예상되는 반응을 기록합니다.
- Control: 1..1

   - AdverseReaction.identifier
    - Definition: 리소스에 대한 직접적인 URL 참조가 적절하지 않은 경우 (예 : CDA 문서 또는 서면 / 인쇄 된 문서) 처리 된 비즈니스에서 정의한이 반응과 관련된 식별자를 기록합니다.
    - Control: 0..*
    - Type: [Identifier](https://www.hl7.org/fhir/DSTU1/datatypes.html#Identifier)

  - AdverseReaction.date
    - Definition: 반응이 시작된 날짜 (시간).
    - Control: 0..1
    - Type:	[dateTime](https://www.hl7.org/fhir/DSTU1/datatypes.html#dateTime)

  - AdverseReaction.subject
    - Definition: 부작용의 대상.
    - Control: 1..1
    - Type: [Resource](https://www.hl7.org/fhir/DSTU1/references.html#Resource)([Patient](https://www.hl7.org/fhir/DSTU1/patient.html))

  - AdverseReaction.didNotOccurFlag
    - Definition: true 인 경우 반응이 발생하지 않았 음을 나타냅니다.
    - Control: 1..1
    - Type:	boolean
    - [Is Modifier](https://www.hl7.org/fhir/DSTU1/conformance-rules.html#ismodifier):	true
    - Requirements: 일반적으로 다른 긍정적 인 반응 기록과 일 때 유용합니다. ex, "환자는 A와 B에 반응하지만 C에 노출되면 반응하지 않았습니다."

  - AdverseReaction.recorder
    - Definition: 반응 기록의 정보 책임자를 나타냅니다.
    - Control: 0..1
    - Type: [Resource](https://www.hl7.org/fhir/DSTU1/references.html#Resource)([Practitioner](https://www.hl7.org/fhir/DSTU1/practitioner.html) | [Patient](https://www.hl7.org/fhir/DSTU1/patient.html))


##### AdverseReaction.symptom
- Definition: 반응의 일부로 관찰 된 증상 및 증상.
- Control: 	0..*
- Aliases:	Signs; Symptoms; Manifestations

  - AdverseReaction.symptom.code
    - Definition: 관찰 된 특정 징후 또는 증상을 나타냅니다.
    - Control: 	1..1
    - Binding:	SymptomType: see [ICD-10 Reaction codes](http://apps.who.int/classifications/icd10/browse/2010/en)
    - Type: [CodeableConcept](https://www.hl7.org/fhir/DSTU1/datatypes.html#CodeableConcept)

  - AdverseReaction.symptom.severity
    - Definition: 증상이나 징후의 심각도.
    - Control: 0..1
    - Binding: ReactionSeverity : 부작용의 심각도.([http://hl7.org/fhir/reactionSeverity](https://www.hl7.org/fhir/DSTU1/reactionSeverity.html))
    - 	Type: 	[Code](https://www.hl7.org/fhir/DSTU1/datatypes.html#code)


##### AdverseReaction.exposure
- Definition: 반응 발생 이전의 물질에 대한 노출을 나타냅니다.
- Control: 	0..*
- Commnets: 반응을 일으킬 수있는 여러 가지 원인을 나타 내기 위해 여러 번의 반복되어 사용됩니다.

  - AdverseReaction.exposure.date
    - Definition: 반응과 관련이있는 것으로 의심되는 노출 초기 날짜를 나타냅니다.
    - Control: 0..1
    - Type: dateTime

  - AdverseReaction.exposure.type
    - Definition: 노출유형: Drug Administration, Immunization, Coincidental.
    - Control: 0..1
    - Binding: ExposureType: 부작용을 일으킨 노출 유형 ([http://hl7.org/fhir/exposureType](https://www.hl7.org/fhir/DSTU1/exposureType.html))
    - Type: [Code](https://www.hl7.org/fhir/DSTU1/datatypes.html#code)

  - AdverseReaction.exposure.causalityExpectation
    - Definition: 노출에 대한 반응의 확신도를 나타냅니다.
    - Control: 0..1
    - Binding: CausalityExpectation: 주어진 노출로 인한 반응 가능성([http://hl7.org/fhir/causality](https://www.hl7.org/fhir/DSTU1/causalityExpectation.html))
    - Type: [Code](https://www.hl7.org/fhir/DSTU1/datatypes.html#code)

  - AdverseReaction.exposure.substance
    - Definition: 부작용을 일으킨 것으로 추정되는 물질
    - Control: 0..1
    - Type: [Resource](https://www.hl7.org/fhir/DSTU1/references.html#Resource)([Substance](https://www.hl7.org/fhir/DSTU1/substance.html))

``` JSON
{
  "resourceType": "AdverseReaction",
  "text": {
    "status": "generated",
    "div": "<div>Anaphylaxis Reaction to a bee sting</div>"
  },
  "date": "2012-09-17",
  "subject": {
    "reference": "Patient/example"
  },
  "didNotOccurFlag": false,
  "recorder": {
    "reference": "Practitioner/example"
  },
  "symptom": [
    {
      "code": {
        "coding": [
          {
            "system": "http://hl7.org/fhir/sid/icd-10",
            "code": "T78.2",
            "display": "Anaphylactic shock, unspecified"
          }
        ],
        "text": "Anaphylaxis reaction"
      },
      "severity": "moderate"
    }
  ],
  "exposure": [
    {
      "date": "2012-09-17",
      "type": "coincidental",
      "substance": {
        "reference": "Substance/example"
      }
    }
  ]
}
```
