graph TD
    %% Estilos y colores
    classDef security fill:#2d3748,stroke:#4a5568,color:#fff,stroke-width:2px;
    classDef process fill:#2b6cb0,stroke:#3182ce,color:#fff,stroke-width:2px;
    classDef ai fill:#2c7a7b,stroke:#319795,color:#fff,stroke-width:2px;
    classDef decision fill:#744210,stroke:#d69e2e,color:#fff,stroke-width:2px;
    classDef output fill:#276749,stroke:#38a169,color:#fff,stroke-width:2px;

    %% Nodos del Flujograma
    Start([Inicio: Caso recibido en Consultorio]) --> Auth[Login Criptografiado / Acceso Verificado]:::security
    Auth --> Input[Estudiante ingresa datos del caso bruto]:::process
    
    Input --> LocalAI[IA Local / Script de Anonimización]:::process
    
    LocalAI --> Check{¿Datos sensibles <br/> de identificación?}:::decision
    
    Check -->|Sí| Mask[Reemplazo por Placeholders <br/> Ej: PACIENTE_1, FECHA_X]:::process
    Check -->|No| SafePass[Conservar hechos jurídicos y fechas]:::process
    
    Mask --> SafePass
    
    SafePass --> Formatter[Herramienta de Abstracción en Lenguaje Formal]:::process
    
    Formatter --> ExternalAI[IA Externa / Modelo de Redacción]:::ai
    
    ExternalAI --> Draft[Generación de Borrador de Tutela Estructurado]:::ai
    
    Draft --> Reintegrate[Script de Des-seudonimización <br/> Inserción automática de Placeholders reales]:::process
    
    Reintegrate --> Review[Filtro de Compliance & Visto Bueno Humano <br/> Prevención de alucinaciones]:::decision
    
    Review -->|Aprobado| Final[Documento Final Listo para Radicación]:::output
    Review -->|Requiere Ajustes| Input
    
    Final --> End([Fin: Bienestar y Eficiencia Estudiantil])
