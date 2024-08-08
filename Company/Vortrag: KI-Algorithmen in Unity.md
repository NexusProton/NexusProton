### Vortrag: KI-Algorithmen in Unity und Weitere Ansätze zur Erweiterung

**Datum:** 7. August 2024  
**Vortragende:** Kai und Aida

---

#### **Einleitung**

**Kai:** Herzlich willkommen zum heutigen Vortrag. Aida und ich werden über die Integration von KI-Algorithmen in Unity sprechen und mögliche Ansätze zur Erweiterung unserer Spieleprojekte vorstellen.

**Aida:** Genau, wir werden Ihnen zeigen, wie wir KI nutzen können, um unsere Spiele intelligenter und dynamischer zu gestalten. Dabei gehen wir auf spezifische Algorithmen und Techniken ein, die in Unity implementiert werden können.

---

#### **1. Grundlagen der KI in Unity**

**Kai:** Unity bietet eine flexible Plattform zur Implementierung von KI-Algorithmen. Einige grundlegende Ansätze umfassen:

- **Finite State Machines (FSMs):** Modellierung von Zustandsübergängen für NPCs.
- **Behavior Trees:** Strukturierte, hierarchische Darstellung von NPC-Verhalten.
- **NavMesh:** Navigation und Pfadfindung in 3D-Umgebungen.
- **Decision Trees:** Entscheidungsfindung basierend auf Bedingungen und Aktionen.

**Aida:** Diese Techniken ermöglichen es, NPCs (Nicht-Spieler-Charaktere) realistischer und interaktiver zu gestalten. Sie können zum Beispiel die Bewegungen von Gegnern steuern, die Reaktionen auf Spieleraktionen bestimmen und komplexe Verhaltensmuster erstellen.

---

#### **2. Implementierung von KI-Algorithmen**

**Kai:** Lassen Sie uns einige dieser Techniken genauer betrachten und wie sie in Unity implementiert werden können.

- **NavMesh Navigation:**
  ```csharp
  using UnityEngine;
  using UnityEngine.AI;

  public class EnemyAI : MonoBehaviour
  {
      public Transform[] waypoints;
      private NavMeshAgent agent;
      private int currentWaypointIndex;

      void Start()
      {
          agent = GetComponent<NavMeshAgent>();
          agent.SetDestination(waypoints[0].position);
      }

      void Update()
      {
          if (!agent.pathPending && agent.remainingDistance < 0.5f)
          {
              currentWaypointIndex = (currentWaypointIndex + 1) % waypoints.Length;
              agent.SetDestination(waypoints[currentWaypointIndex].position);
          }
      }
  }
  ```
  - **Explanation:** Dieses Skript ermöglicht einem NPC, sich zwischen vordefinierten Wegpunkten zu bewegen.

- **Behavior Trees:**
  - **Aida:** Behavior Trees bieten eine flexible Möglichkeit, komplexe Verhaltensweisen zu definieren. Es gibt mehrere Unity-Plugins wie „Behavior Designer“ und „NodeCanvas“, die die Erstellung und Verwaltung von Behavior Trees erleichtern.

**Aida:** Ein weiteres Beispiel ist die Implementierung eines einfachen Entscheidungsbaums:

- **Decision Trees:**
  ```csharp
  public class DecisionNode
  {
      public string question;
      public DecisionNode trueNode;
      public DecisionNode falseNode;

      public DecisionNode(string question)
      {
          this.question = question;
      }
  }

  public class DecisionTree : MonoBehaviour
  {
      private DecisionNode root;

      void Start()
      {
          root = new DecisionNode("Is the player visible?");
          root.trueNode = new DecisionNode("Chase the player");
          root.falseNode = new DecisionNode("Patrol area");
      }

      void Update()
      {
          string decision = EvaluateDecisionTree(root);
          Debug.Log("Decision: " + decision);
      }

      string EvaluateDecisionTree(DecisionNode node)
      {
          // Hier würde die Bedingungsprüfung basierend auf Spielzuständen erfolgen
          return node.question == "Is the player visible?" ? node.trueNode.question : node.falseNode.question;
      }
  }
  ```
  - **Explanation:** Dieser einfache Entscheidungsbaum entscheidet, ob ein NPC den Spieler verfolgen oder patrouillieren soll, basierend auf einer Bedingung.

---

#### **3. Erweiterte KI-Ansätze**

**Kai:** Neben den grundlegenden Techniken gibt es fortgeschrittene Ansätze, die unsere Spiele noch realistischer und herausfordernder machen können:

- **Machine Learning (ML):**
  - Verwendung von Unity ML-Agents, um NPCs durch Reinforcement Learning zu trainieren.
  - Beispiel: Training eines Agenten, der lernt, Hindernisse zu vermeiden und Ziele zu erreichen.

- **Neural Networks:**
  - Integration von neuronalen Netzwerken für komplexe Entscheidungsfindungen.
  - Beispiel: Einsatz eines neuronalen Netzwerks zur Vorhersage von Spielerbewegungen und Anpassung des NPC-Verhaltens.

**Aida:** Hier ist ein Beispiel für die Implementierung von Unity ML-Agents:

- **Unity ML-Agents:**
  ```csharp
  using Unity.MLAgents;
  using Unity.MLAgents.Sensors;
  using Unity.MLAgents.Actuators;

  public class AgentAI : Agent
  {
      public Transform target;

      public override void OnEpisodeBegin()
      {
          // Reset agent and target positions
      }

      public override void CollectObservations(VectorSensor sensor)
      {
          sensor.AddObservation(transform.localPosition);
          sensor.AddObservation(target.localPosition);
      }

      public override void OnActionReceived(ActionBuffers actions)
      {
          float moveX = actions.ContinuousActions[0];
          float moveZ = actions.ContinuousActions[1];
          transform.localPosition += new Vector3(moveX, 0, moveZ) * Time.deltaTime;
      }
  }
  ```
  - **Explanation:** Dieses Skript definiert einen Agenten, der durch Reinforcement Learning trainiert werden kann, um ein Ziel zu erreichen.

---

#### **4. Herausforderungen und Lösungsansätze**

**Kai:** Die Implementierung von KI-Algorithmen bringt auch Herausforderungen mit sich:

- **Performance:** KI-Berechnungen können rechenintensiv sein und die Performance des Spiels beeinträchtigen.
- **Balancing:** KI muss gut ausbalanciert sein, um das Spielerlebnis nicht zu frustrierend oder zu einfach zu gestalten.
- **Debugging:** Fehler in KI-Algorithmen sind oft schwer zu erkennen und zu beheben.

**Aida:** Lösungsansätze umfassen:

- **Optimierung:** Effiziente Algorithmen und Datenstrukturen verwenden.
- **Testing:** Umfangreiche Tests und Debugging-Tools nutzen.
- **Balancing:** Regelmäßige Anpassungen und Spieler-Feedback einholen.

---

#### **5. Zusammenfassung und Q&A**

**Kai:** Zusammenfassend lässt sich sagen, dass die Integration von KI in Unity zahlreiche Möglichkeiten bietet, um unsere Spiele intelligenter und dynamischer zu gestalten. Die vorgestellten Algorithmen und Techniken sind nur der Anfang, und wir freuen uns darauf, gemeinsam weiter an innovativen Lösungen zu arbeiten.

**Aida:** Wir stehen jetzt für Fragen zur Verfügung. Wenn es keine gibt, dann lasst uns das Gelernte in den nächsten Projekten anwenden und kontinuierlich verbessern.

---

**Q&A:**
- **Frage 1:** Wie können wir sicherstellen, dass die KI in unseren Spielen nicht zu vorhersehbar wird?
  - **Antwort von Kai:** Durch den Einsatz von zufälligen Elementen und adaptiven Algorithmen, die sich an das Verhalten der Spieler anpassen.

- **Frage 2:** Welche Tools können wir nutzen, um die KI-Performance zu überwachen und zu optimieren?
  - **Antwort von Aida:** Tools wie Unity Profiler, ML-Agents Toolkit und externe Monitoring-Tools wie TensorBoard können hilfreich sein.

- **Frage 3:** Wie integrieren wir Machine Learning-Modelle, die außerhalb von Unity trainiert wurden?
  - **Antwort von Kai:** Durch die Nutzung von ONNX (Open Neural Network Exchange) können wir Modelle, die in Python oder anderen Frameworks trainiert wurden, in Unity importieren und verwenden.

---

**Ende des Vortrags:**

**Kai:** Vielen Dank für eure Aufmerksamkeit. Wir freuen uns auf die Zusammenarbeit und die spannenden Projekte, die vor uns liegen.

**Aida:** Danke, und lasst uns gemeinsam großartige Spiele mit intelligenter KI entwickeln!

---

**Protokollführer:** Tobi
