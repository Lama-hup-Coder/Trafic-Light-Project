## 🧠 Logic Core: The "Compass" Pattern
The most critical part of this project is how the traffic light knows its next state, especially when transitioning through the **Orange** light. I used a "Compass" variable to store the future destination before entering the transition state.

```csharp
// The Enum that defines our states
public enum enLightState { Red, Orange, Green }

// The "Golden" logic inside the Timer Tick or State Changer
private enLightState _CurrentState = enLightState.Red;
private enLightState _LightAfterOrange = enLightState.Green; // The Compass

private void _ChangeLight()
{
    switch (_CurrentState)
    {
        case enLightState.Red:
            _LightAfterOrange = enLightState.Green; // Prepare next destination
            _CurrentState = enLightState.Orange;
            break;

        case enLightState.Green:
            _LightAfterOrange = enLightState.Red; // Prepare next destination
            _CurrentState = enLightState.Orange;
            break;

        case enLightState.Orange:
            _CurrentState = _LightAfterOrange; // Go to the pre-planned destination
            break;
    }
    
    // Update UI and Raise Events here...
    UpdateUI();
}
### 💡 الخلاصة البرمجية (بالعربية)
الفكرة الأساسية هنا هي استخدام متغير "البوصلة" (`_LightAfterOrange`). 
بدلاً من أن نجعل اللون البرتقالي "يخمن" اللون التالي، نقوم بتحديد الوجهة مسبقاً قبل الانتقال للبرتقالي. 
هذا يضمن تتابعاً صحيحاً ودائماً للإشارة (أحمر -> برتقالي -> أخضر) والعكس، دون أي تداخل في الحالات.
